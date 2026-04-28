day29/
├── base/                    # 基础工具类
│   ├── CurrentThread.*      # 当前线程信息
│   ├── Latch.h              # 线程同步工具
│   └── common.h             # 通用宏定义
│
├── tcp/                     # TCP 网络层 (Reactor 核心)
│   ├── EventLoop.*          # 事件循环 (主 Reactor)
│   ├── Epoller.*            # epoll 封装
│   ├── Channel.*            # 文件描述符事件封装
│   ├── Acceptor.*           # 连接接受器
│   ├── TcpServer.*          # TCP 服务器
│   ├── TcpConnection.*      # TCP 连接管理
│   ├── Buffer.*             # 缓冲区
│   ├── EventLoopThread.*    # 单线程事件循环
│   └── EventLoopThreadPool.* # 线程池
│
├── http/                    # HTTP 协议层 ⭐
│   ├── HttpServer.*         # ⭐⭐⭐ HTTP 服务器 (核心)
│   ├── HttpContext.*        # HTTP 请求解析上下文 (状态机)
│   ├── HttpRequest.*        # HTTP 请求对象
│   └── HttpResponse.*       # HTTP 响应对象
│
├── timer/                   # 定时器模块
│   ├── TimerQueue.*         # 定时器队列
│   └── Timer.*              # 定时器
│
├── log/                     # 日志模块
│   ├── AsyncLogging.*       # 异步日志
│   ├── LogFile.*            # 日志文件
│   ├── Logging.*            # 日志接口
│   └── LogStream.*          # 日志流
│
├── static/                  # 静态资源文件
│   ├── index.html
│   ├── mhw.html
│   └── fileserver.html
│
└── test/                    # 测试程序
    ├── http_server.cpp      # ⭐⭐ HTTP 服务器示例 (入口)
    ├── echo_server.cpp      # Echo 服务器示例
    ├── test_httpcontext.cpp # HTTP 解析测试
    └── test_logstream.cpp   # 日志流测试