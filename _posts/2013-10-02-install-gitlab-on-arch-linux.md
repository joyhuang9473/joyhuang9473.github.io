---
layout: post
title: 'Install Gitlab on Arch Linux'
date: 2013-10-02 14:06
comments: true
tags: [GitLab, Arch]
---
## Gitlab Wiki ##
[https://github.com/gitlabhq/gitlabhq/blob/master/doc/install/installation.md](https://github.com/gitlabhq/gitlabhq/blob/master/doc/install/installation.md "gitlab wiki")

## Reference ##
[https://gist.github.com/axilleas/3305554](https://gist.github.com/axilleas/3305554 "reference")

## Begin ##

### 1.Packages / Dependencies : Install the required packages ###

    sudo pacman -S sudo base-devel zlib libyaml openssl gdbm readline ncurses libffi curl git openssh redis libxml2 libxslt icu python2 python-docutils cmake

### 2.Ruby ###

Download Ruby and compile it:

    mkdir /tmp/ruby && cd /tmp/ruby
    curl -L --progress ftp://ftp.ruby-lang.org/pub/ruby/2.1/ruby-2.1.2.tar.gz | tar xz
    cd ruby-2.1.2
    ./configure
    make
    sudo make install

Install the Bundler Gem:

    sudo gem install bundler --no-ri --no-rdoc

### 3.System Users ###

Create a git user for Gitlab:

    sudo userdel git
    sudo useradd -m -s /bin/false git
    sudo chmod 755 /home/git

### 4.GitLab shell ###

GitLab Shell is an ssh access and repository management software developed specially for GitLab.

    # Go to home directory
    cd /home/git

    # Clone gitlab shell
    sudo -u git -H git clone https://github.com/gitlabhq/gitlab-shell.git

    cd gitlab-shell

    sudo -u git -H cp config.yml.example config.yml

    # Edit config and replace gitlab_url
    # with something like 'http://domain.com/'
    sudo -u git -H editor config.yml

    # Do setup
    sudo -u git -H ./bin/install

### 5.Database ###

To setup the MySQL

    sudo pacman -S mysql
    sudo systemctl start mysqld
    sudo mysql_secure_installation

    # Login to MySQL
    mysql -u root -p

    # Create a user for GitLab
    # change $password in the command below to a real password you pick
    mysql> CREATE USER 'gitlab'@'localhost' IDENTIFIED BY '$password';

    # Create the GitLab production database
    mysql> CREATE DATABASE IF NOT EXISTS `gitlabhq_production` DEFAULT CHARACTER SET `utf8` COLLATE `utf8_unicode_ci`;

    # Grant the GitLab user necessary permissions on the table.
    mysql> GRANT SELECT, LOCK TABLES, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER ON `gitlabhq_production`.* TO 'gitlab'@'localhost';

    # Quit the database session
    mysql> \q

### 6.GitLab ###

We'll install GitLab into home directory of the user "git"

    cd /home/git

#### Clone the Source ####

    # Clone GitLab repository
    sudo -u git -H git clone https://github.com/gitlabhq/gitlabhq.git gitlab

    # Go to gitlab dir
    cd /home/git/gitlab

    # Checkout to stable release
    sudo -u git -H git checkout 7-0-stable

Note: You can change 7-0-stable to master if you want the bleeding edge version, but never install master on a production server!

#### Configure it ####

    cd /home/git/gitlab

    # Copy the example GitLab config
    sudo -u git -H cp config/gitlab.yml.example config/gitlab.yml

    # Make sure to change "localhost" to the fully-qualified domain name of your
    # host serving GitLab where necessary
    sudo -u git -H editor config/gitlab.yml

    # Make sure GitLab can write to the log/ and tmp/ directories
    sudo chown -R git log/
    sudo chown -R git tmp/
    sudo chmod -R u+rwX  log/
    sudo chmod -R u+rwX  tmp/

    # Create directory for satellites
    sudo -u git -H mkdir /home/git/gitlab-satellites

    # Create directories for sockets/pids and make sure GitLab can write to them
    sudo -u git -H mkdir tmp/pids/
    sudo -u git -H mkdir tmp/sockets/
    sudo chmod -R u+rwX  tmp/pids/
    sudo chmod -R u+rwX  tmp/sockets/

    # Create public/uploads directory otherwise backup will fail
    sudo -u git -H mkdir public/uploads
    sudo chmod -R u+rwX  public/uploads

    # Copy the example Unicorn config
    sudo -u git -H cp config/unicorn.rb.example config/unicorn.rb

    # Enable cluster mode if you expect to have a high load instance
    # Ex. change amount of workers to 3 for 2GB RAM server
    sudo -u git -H editor config/unicorn.rb

    # Copy the example Rack attack config
    # sudo -u git -H cp config/initializers/rackattack.rb.example config/initializers/rackattack.rb**

    # Enable rack attack middleware
    # Find and uncomment the line 'config.middleware.use Rack::Attack'
    sudo -u git -H editor config/application.rb

    # Configure Git global settings for git user, useful when editing via web
    # Edit user.email according to what is set in gitlab.yml
    sudo -u git -H git config --global user.name "GitLab"
    sudo -u git -H git config --global user.email "gitlab@localhost"
    sudo -u git -H git config --global core.autocrlf input

#### Configure GitLab DB settings ####

    # Mysql
    sudo -u git cp config/database.yml.mysql config/database.yml

    # Make sure to update username/password in config/database.yml.
    # You only need to adapt the production settings (first part).
    # If you followed the database guide then please do as follows:
    # Change 'root' to 'gitlab'
    # Change 'secure password' with the value you have given to $password
    # You can keep the double quotes around the password
    sudo -u git -H editor config/database.yml

    # Make config/database.yml readable to git only
    sudo -u git -H chmod o-rwx config/database.yml

#### Install Gems ####

    cd /home/git/gitlab

    # For MySQL (note, the option says "without ... postgres")
    sudo -u git -H bundle install --deployment --without development test postgres aws

#### Initialize Database and Activate Advanced Features ####

    sudo systemctl start redis
    sudo -u git -H bundle exec rake gitlab:setup RAILS_ENV=production

    # Type 'yes' to create the database.

    # When done you see 'Administrator account created:'

#### Install Init Script ####

Download the init script (will be /etc/init.d/gitlab):

    # @Notice : 在 ArchLinux ， 這份 Init Script 無法正常執行，之後需要手動下 command
    # 即使如此，我仍 cp 這份 script 到 /etc/init.d/ [需創建資料夾] ，因為後面的 Check Application Status
    # 似乎會檢查 /etc/init.d/gitlab 是否存在
    sudo cp lib/support/init.d/gitlab /etc/init.d/gitlab
    sudo chmod +x /etc/init.d/gitlab

#### Setup Logrotate ####

    sudo cp lib/support/logrotate/gitlab /etc/logrotate.d/gitlab

#### Check Application Status ####

Check if GitLab and its environment are configured correctly:

    sudo -u git -H bundle exec rake gitlab:env:info RAILS_ENV=production

#### Compile Assets ####

    sudo -u git -H bundle exec rake assets:precompile RAILS_ENV=production

#### Starts Unicorn and Sidekiq ####

    # Remove old socket if it exists
    rm -f "/home/git/gitlab/tmp/sockets"/gitlab.socket 2>/dev/null
    # Start the webserver
    cd /home/git/gitlab
    sudo -u git -H bundle exec unicorn_rails -D -c "/home/git/gitlab/config/unicorn.rb" -E "production"
     
    # If sidekiq is already running, don't start it again.
    # Starting the GitLab Sidekiq event dispatcher
    sudo -u git -H RAILS_ENV=production bundle exec rake sidekiq:start

### 7.Nginx ##

#### Installation ####

    sudo pacman -S nginx

#### Site Configuration ####

Download an example site config:

    sudo cp lib/support/nginx/gitlab /etc/nginx/sites-available/gitlab
    sudo ln -s /etc/nginx/sites-available/gitlab /etc/nginx/sites-enabled/gitlab

Make sure to edit the config file to match your setup:

    # Change YOUR_SERVER_FQDN to the fully-qualified
    # domain name of your host serving GitLab.
    sudo vim /etc/nginx/sites-available/gitlab

Include /etc/nginx/sites-enabled/gitlab

    sudo vim /etc/nginx/nginx.conf

    ---
    http {
    ...
        include /etc/nginx/sites-enabled/*;
    ...

## Start Nginx ##

    sudo systemctl start nginx

## Double-check Application Status ##

To make sure you didn't miss anything run a more thorough check with:

    sudo systemctl start redis
    sudo -u git -H bundle exec rake sidekiq:start RAILS_ENV=production
    sudo -u git -H bundle exec rake gitlab:check RAILS_ENV=production

If all items are green, then congratulations on successfully installing GitLab! However there are still a few steps left.

## Done! ##

Visit YOUR_SERVER for your first GitLab login. The setup has created an admin account for you. You can use it to log in:

    admin@local.host
    5iveL!fe

Important Note: Please go over to your profile page and immediately change the password, so nobody can access your GitLab by using this login information later on.

Enjoy!