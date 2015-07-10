---
layout: post
title: 'Install Redmine on Arch Linux'
date: 2014-06-28 05:20
comments: true
tags: [rails, Redmine]
---
之前參加一個敏捷專案管理課程知道的，是一個**專案管理工具**，包含 issue tracking 等功能，而架設的門檻的確有點高，過程中個人就弄爆好幾次，特別在此記錄一些小問題。

[Redmine](http://www.redmine.org/)

[Redmine - ArchWiki](https://wiki.archlinux.org/index.php/redmine)

### Prerequisites ###

- Ruby       (1.9.3)
- Database   (MariaDB)
- Web Server (WEBrick)

在需求上，需要 Ruby, Database, Web Server，而在 Ruby 版本 和 Database, Web Server 的選擇上其實還蠻多的，個人是使用了 Ruby 1.9.3 版、MariaDB、WEBrick。

### Optional Prerequisites ###

- SCM (Git)
- ImageMagick
- *Ruby OpenID Library (未使用)

而在 Optional Prerequisites，比較特別的是 ImageMagick，查看 Arch wiki：

> ImageMagick is necessary to enable Gantt export to png image.

原來是匯出圖片用的，雖然不知道會不會用到，不過就還是裝，但悲劇就從這裡發生了，留到後面再提吧 ==
而 SCM （Source Code Management）選擇了 git

ok，開始進入安裝

# Prerequisites

---

###Ruby(& RVM)

[RVM - ArchWiki](https://wiki.archlinux.org/index.php/RVM)

個人使用 rvm 安裝了 1.9.3 版的 Ruby，而這方法似乎也是被大家所推薦的

而 rvm 的安裝還分兩種，Single-user installation 和 Multi-user installation

而我選擇 Single-user installation ，並新增了一個 redmine 使用者來安裝:

    [sudoer@localhost ~]$ sudo useradd -m redmine

切換到 redmine user 做安裝:

    [sudoer@localhost ~]$ sudo su redmine
    [redmine@localhost ~]$ curl -L get.rvm.io > rvm-install
    [redmine@localhost ~]$ bash < ./rvm-install
    [redmine@localhost ~]$ curl -L get.rvm.io | bash -s stable
    [redmine@localhost ~]$ [[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm"
    [redmine@localhost ~]$ source ~/.bash_profile

測試 rvm:

    [redmine@localhost ~]$ type rvm

出現:

    rvm is a function

有一點要注意的是：

> In order to work, RVM has some of its own dependencies that need to be installed.

記得查看有哪些 dependencies

    [redmine@localhost ~]$ rvm requirements

註：[How To Install Ruby on Rails on Arch Linux with RVM](https://www.digitalocean.com/community/tutorials/how-to-install-ruby-on-rails-on-arch-linux-with-rvm)

rvm 安裝完成，指定安裝 ruby 1.9.3

    [redmine@localhost ~]$ rvm install 1.9.3
    [redmine@localhost ~]$ rvm use 1.9.3 --default

那麼 ruby 的安裝就到這了

### Database

這就 pacman 選擇自己想要的資料庫去安裝了

回到 sudoer ，安裝 MariaDB

    [sudoer@localhost ~]$ sudo pacman -S mysql

### Web Server

個人使用 WEBrick，而 WEBrick 本身就和 Ruby 綁在一起，所以不需另外自己安裝了，但網路上也有人說 WEBrick 的效率較差，建議用 Mongrel 或 Unicorn ，而這就留到以後再嘗試囉。

# Optional Prerequisites

---

### SCM (Git)

    [sudoer@localhost ~]$ sudo pacman -S git

### ImageMagick

問題來了，因為 "Rmagick failing to build on Arch due to HDRI Imagemagick"，為避免後續的安裝問題，我採用了 [Sharpe End : Rmagick failing to build on Arch due to HDRI Imagemagick](http://sharpeend.impcode.com/2014/02/rmagick-failing-to-build-on-arch-due-to.html) 這篇文章所介紹的方法而不是 Arch-Wiki 上的 imagemagick

安裝 AUR 的 [imagemagick-no-hdri](https://aur.archlinux.org/packages/imagemagick-no-hdri/)

    [sudoer@localhost ~]$ aurget -S imagemagick-no-hdri

# Installation : Redmine

---

[Installation - ArchWiki](https://wiki.archlinux.org/index.php/redmine#Installation)

切換到 redmine user

> Download the package [redmine](https://aur.archlinux.org/packages/redmine/) from the AUR.

> Build and Installation

這時在家目錄應該會看到一個 redmine-2.5.1 的資料夾

## Database Configuration

**Database Creation**

[Database Creation - ArchWiki](https://wiki.archlinux.org/index.php/redmine#Database_Creation)

**Database Access Configuration**

    [redmine@localhost ~]$ cd redmine-2.5.1/config
    [redmine@localhost config]$ cp database.yml.example database.yml
    [redmine@localhost config]$ vim database.yml

    production:
      adapter: mysql2
      database: redmine
      host: localhost
      port: 3307   #If your server is not running on the standard port (3306), set it here, otherwise this line is unnecessary.
      username: redmine
      password: my_password


參考 [Database Access Configuration - ArchWiki](https://wiki.archlinux.org/index.php/redmine#Database_Access_Configuration)

## Adding Additional Gems (Optional)

回到 redmine-2.5.1 根目錄

    [redmine@localhost redmine-2.5.1]$ vim Gemfile.local

    gem 'puma'

## Gems Installation

> Redmine uses Bundler to manage gems dependencies. So, you need to install Bundler first

    [redmine@localhost redmine-2.5.1]$ gem install bundler
    [redmine@localhost redmine-2.5.1]$ bundle install

## Session Store Secret Generation

> Now you must generate a random key that will be used by Rails to encode cookies that stores session data thus preventing their tampering

    [redmine@localhost redmine-2.5.1]$ rake generate_secret_token

## Database Structure Creation

> These command will create tables by running all migrations one by one then create the set of the permissions and the application administrator account, named admin.

    [redmine@localhost redmine-2.5.1]$ RAILS_ENV=production rake db:migrate

## Database Population with Default Data

> insert the default configuration data in database, like basic types of task, task states, groups

    [redmine@localhost redmine-2.5.1]$ RAILS_ENV=production rake redmine:load_default_data

## Test the installation

> test your new installation using WEBrick web server run the following in the Redmine folder

    [redmine@localhost redmine-2.5.1]$ ruby script/rails server webrick -e production

ctr-D 結束

到這裡整個 redmine 的安裝就結束囉

## Creating a Systemd Unit

而為了方便啟動 redmine ，新增了一個 systemd unit file：

/etc/systemd/system/redmine.service

    [Unit]
    Description=Redmine server
    After=syslog.target
    After=network.target

    [Service]
    Type=simple
    User=redmine2
    Group=redmine2
    Environment=GEM_HOME=/home/redmine/.rvm/gems/ruby-1.9.3-p547/gems
    ExecStart=/home/redmine/.rvm/bin/rvm-auto-ruby /home/redmine/redmine-2.5.1/script/rails server webrick -e production

    # Give a reasonable amount of time for the server to start up/shut down
    TimeoutSec=300

    [Install]
    WantedBy=multi-user.target

以後就可以用 systemctl 來啟動 redmine 了

---

# 啟動 Redmine

    [sudoer@localhost ~]$ sudo systemctl start redmine

# 關閉 Redmine

我現在的方法是直接查詢 pid 並 kill 掉，這樣的方式還不是很好，可能就再想想吧

    [sudoer@localhost ~]$ ps -ef | grep script/rails
    redmine   2625     1  0 Jun26 ?        00:01:42 ruby /home/redmine/redmine-2.5.1/script/rails server webrick -e production
    [sudoer@localhost ~]$ kill -9 2625

#Note

[Why can't Phusion Passenger extend my existing Nginx?](https://github.com/phusion/passenger/wiki/Why-can%27t-Phusion-Passenger-extend-my-existing-Nginx%3F)

# Trouble Shooting

problem : Rmagick failing to build on Arch due to HDRI Imagemagick

reason : RMagick gem without support for High Dynamic Range in ImageMagick

solution : 
1) http://sharpeend.impcode.com/2014/02/rmagick-failing-to-build-on-arch-due-to.html
2) Arch wiki Troubleshooting

log :

    [redmine@localhost redmine-2.5.1]$ gem install rmagick -v '2.13.2'
    Building native extensions.  This could take a while...
    ERROR:  Error installing rmagick:
    ERROR: Failed to build gem native extension.

    /home/redmine/.rvm/rubies/ruby-2.0.0-p481/bin/ruby extconf.rb
    checking for Ruby version >= 1.8.5... yes
    checking for gcc... yes
    checking for Magick-config... yes
    checking for ImageMagick version >= 6.4.9... yes
    checking for HDRI disabled version of ImageMagick... no

    Can't install RMagick 2.13.2.
    RMagick does not work when ImageMagick is configured for High Dynamic Range Images.
    Don't use the --enable-hdri option when configuring ImageMagick.

    *** extconf.rb failed ***
    Could not create Makefile due to some reason, probably lack of necessary
    libraries and/or headers.  Check the mkmf.log file for more details.  You may
    need configuration options.

    Provided configuration options:
        --with-opt-dir
        --without-opt-dir
        --with-opt-include
        --without-opt-include=${opt-dir}/include
        --with-opt-lib
        --without-opt-lib=${opt-dir}/lib
        --with-make-prog
        --without-make-prog
        --srcdir=.
        --curdir
        --ruby=/home/redmine/.rvm/rubies/ruby-2.0.0-p481/bin/ruby

    extconf failed, exit code 1

    Gem files will remain installed in /home/redmine/.rvm/gems/ruby-2.0.0-p481/gems/rmagick-2.13.2 for inspection.
    Results logged to /home/redmine/.rvm/gems/ruby-2.0.0-p481/extensions/x86_64-linux/2.0.0/rmagick-2.13.2/gem_make.out

---

problem : pg gem won't install

solution : install postgresql

link : http://stackoverflow.com/questions/19262312/installing-pg-gem-failure-to-build-native-extension/19620569#19620569

log :

    Gem::Ext::BuildError: ERROR: Failed to build gem native extension.

        /home/redmine/.rvm/rubies/ruby-2.0.0-p481/bin/ruby extconf.rb 
    checking for pg_config... no
    No pg_config... trying anyway. If building fails, please try again with
     --with-pg-config=/path/to/pg_config
    checking for libpq-fe.h... no
    Can't find the 'libpq-fe.h header
    *** extconf.rb failed ***
    Could not create Makefile due to some reason, probably lack of necessary
    libraries and/or headers.  Check the mkmf.log file for more details.  You may
    need configuration options.

    Provided configuration options:
        --with-opt-dir
        --without-opt-dir
        --with-opt-include
        --without-opt-include=${opt-dir}/include
        --with-opt-lib
        --without-opt-lib=${opt-dir}/lib
        --with-make-prog
        --without-make-prog
        --srcdir=.
        --curdir
        --ruby=/home/redmine/.rvm/rubies/ruby-2.0.0-p481/bin/ruby
        --with-pg
        --without-pg
        --with-pg-config
        --without-pg-config
        --with-pg_config
        --without-pg_config
        --with-pg-dir
        --without-pg-dir
        --with-pg-include
        --without-pg-include=${pg-dir}/include
        --with-pg-lib
        --without-pg-lib=${pg-dir}/

    extconf failed, exit code 1

    Gem files will remain installed in /home/redmine/.rvm/gems/ruby-2.0.0-p481/gems/pg-0.17.1 for inspection.
    Results logged to /home/redmine/.rvm/gems/ruby-2.0.0-p481/extensions/x86_64-linux/2.0.0/pg-0.17.1/gem_make.out
    An error occurred while installing pg (0.17.1), and Bundler cannot continue.
    Make sure that `gem install pg -v '0.17.1'` succeeds before bundling.

---

problem : mysql is not part of the bundle. Add it to Gemfile.

solution : 修改 database.yml 的 adapter 為 mysql2

    production:
      adapter: mysql2
      database: redmine

log :

    [redmine redmine-2.5.1]$ RAILS_ENV=production rake db:migrate
    rake aborted!
    LoadError: Please install the mysql adapter: `gem install activerecord-mysql-adapter` (mysql is not part of the bundle. Add it to Gemfile.)
    /home/redmine/.rvm/gems/ruby-1.9.3-p547/gems/bundler-1.6.3/lib/bundler/rubygems_integration.rb:252:in `block in replace_gem'
    /home/redmine/.rvm/gems/ruby-1.9.3-p547/gems/activerecord-3.2.11/lib/active_record/connection_adapters/mysql_adapter.rb:5:in `<top (required)>'
    /home/redmine/.rvm/gems/ruby-1.9.3-p547/gems/activesupport-3.2.11/lib/active_support/dependencies.rb:251:in `require'
    /home/redmine/.rvm/gems/ruby-1.9.3-p547/gems/activesupport-3.2.11/lib/active_support/dependencies.rb:251:in `block in require'
    /home/redmine/.rvm/gems/ruby-1.9.3-p547/gems/activesupport-3.2.11/lib/active_support/dependencies.rb:236:in `load_dependency'
    /home/redmine/.rvm/gems/ruby-1.9.3-p547/gems/activesupport-3.2.11/lib/active_support/dependencies.rb:251:in `require'
    /home/redmine/.rvm/gems/ruby-1.9.3-p547/gems/activerecord-3.2.11/lib/active_record/connection_adapters/abstract/connection_specification.rb:50:in `resolve_hash_connection'
    /home/redmine/.rvm/gems/ruby-1.9.3-p547/gems/activerecord-3.2.11/lib/active_record/connection_adapters/abstract/connection_specification.rb:41:in `resolve_string_connection'
    /home/redmine/.rvm/gems/ruby-1.9.3-p547/gems/activerecord-3.2.11/lib/active_record/connection_adapters/abstract/connection_specification.rb:25:in `spec'
    /home/redmine/.rvm/gems/ruby-1.9.3-p547/gems/activerecord-3.2.11/lib/active_record/connection_adapters/abstract/connection_specification.rb:130:in `establish_connection'
    /home/redmine/.rvm/gems/ruby-1.9.3-p547/gems/activerecord-3.2.11/lib/active_record/railtie.rb:82:in `block (2 levels) in <class:Railtie>'
    /home/redmine/.rvm/gems/ruby-1.9.3-p547/gems/activesupport-3.2.11/lib/active_support/lazy_load_hooks.rb:36:in `instance_eval'
    /home/redmine/.rvm/gems/ruby-1.9.3-p547/gems/activesupport-3.2.11/lib/active_support/lazy_load_hooks.rb:36:in `execute_hook'
    /home/redmine/.rvm/gems/ruby-1.9.3-p547/gems/activesupport-3.2.11/lib/active_support/lazy_load_hooks.

---

problem : [redmine_hipchat_per_project](https://github.com/digitalnatives/redmine_hipchat_per_project) cannot be install

reason : redmine_hipchat_per_project's version

> This version of the plugin is compatible with Redmine 1.4 . If you're using Redmine 2.x, check out the redmine2 branch.

solution : try https://github.com/digitalnatives/redmine_hipchat_per_project/tree/redmine2

log :

    [redmine@localhost redmine-2.5.1]$ ruby script/rails server webrick -e production
    => Booting WEBrick
    => Rails 3.2.17 application starting in production on http://0.0.0.0:3000
    => Call with -d to detach
    => Ctrl-C to shutdown server
    Exiting
    /home/redmine/.rvm/gems/ruby-1.9.3-p547/gems/activesupport-3.2.17/lib/active_support/dependencies.rb:251:in `require': cannot load such file -- dispatcher (LoadError)
        from /home/redmine/.rvm/gems/ruby-1.9.3-p547/gems/activesupport-3.2.17/lib/active_support/dependencies.rb:251:in `block in require'
        from /home/redmine/.rvm/gems/ruby-1.9.3-p547/gems/activesupport-3.2.17/lib/active_support/dependencies.rb:236:in `load_dependency'
        from /home/redmine/.rvm/gems/ruby-1.9.3-p547/gems/activesupport-3.2.17/lib/active_support/dependencies.rb:251:in `require'
        from /home/redmine/redmine-2.5.1/plugins/redmine_hipchat_per_project/init.rb:2:in `<top (required)

---