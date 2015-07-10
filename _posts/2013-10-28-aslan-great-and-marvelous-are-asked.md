---
layout: post
title: 'Aslan 小考試'
date: 2013-10-28 17:26
comments: true
tags: [Aslan]
---
1. 為何Aslan::Core::System已經繼承Aslan::Core::Singletone<Aslan::Core::System>了，還需要設定friend Aslan::Core::Singleton<Aslan::Core::System>呢？我們為什麼沒辦法從Aslan::Core::Singleton<Aslan::Core::System>裡面呼叫Aslan::Core::System::~System()呢？
2. 為什麼InitializeCriticalSection()一定是其他函式庫或著作業系統的函式，不可能是在Aslan或Metal裡面的函式？
3. 那麼CriticalSection又是什麼呢？
4. 為什麼要用Aslan::Type，例如Aslan::Integer這種型別，而不直接用int呢？
5. 初始化建構式跟建構式中賦值有什麼不同之處？
6. 為什麼getenv被標示為不安全的函式？
7. 請說明事件機制？
8. 當Aslan::Core::Logger移至HPP當中之後會有什麼問題？
9. 為什麼檔案結尾都會有一行空行？
10. 為什麼在EventManager當中，要使用(this->m_instance->*(this->m_function))(static_cast<EventType*>(event))去呼叫而不用*(this->m_function)(static_cast<EventType*>(event))呢？
11. 為什麼在EventManager當中，Wrapper、Handler以及Lambda需要存在，它們之間又有什麼差別？
12. 為什麼EventManager當中，LambdaReductionHelper為什麼是需要的？是否能夠去除它呢？
13. 什麼時候會把實作寫在HPP檔案當中？為什麼要這麼做？不這麼做會有什麼問題？
14. 為什麼Aslan::Graphics::Display裡面要有一個native函式，而且回傳void*型別？
15. 為什麼繪圖需要經過容器儲存再統一由Aslan::Manager::Graphics::render完成，好處跟壞處？（這是目前設計的概念）
16. 如何排版建構式清單?迴圈?條件判斷?各種變數以及函式的命名規則?
17. 如何使用 Operator overloading ，Overloading 跟 Overriding 有甚麼不同呢?
18. 如何在 C++ 當中使用匿名函式?
19. 你覺得有那些地方有 Memory leak ? 又該如何修正呢?
20. 在程式當中，nullptr 與 NULL 有甚麼不同嗎?
