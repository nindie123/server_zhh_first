# attempt
### valgrind内存测试
无明显内存泄漏
存在疑似内存泄漏（估计是因为没有服务器优雅关闭导致）
后续完善相关逻辑

### 压测数据
> 压测工具为wrk 相对于webbench测试维度更加全面

zhllj@thefirst:~/server$ wrk -t4 -c100 -d60 http://127.0.0.1:1234
Running 1m test @ http://127.0.0.1:1234
  4 threads and 100 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    15.79ms   71.08ms 951.53ms   97.98%
    Req/Sec     5.38k     1.11k    8.48k    72.27%
  1256136 requests in 1.00m, 1.34GB read
Requests/sec:  20922.50
Transfer/sec:     22.89MB
### 问题分析
首先有些时候似乎这个延迟有点太大了直接就接近 1s
以上测试采用同步日志库，可以采用异步日志库再次测试
#### 采用异步日志库的压测结果
zhllj@thefirst:/mnt/c/Users/zhllj$ wrk -t4 -c100 -d10s http://127.0.0.1:8080/user
Running 10s test @ http://127.0.0.1:8080/user
  4 threads and 100 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency   830.43us    1.00ms  20.61ms   85.77%
    Req/Sec    43.13k     5.02k  105.49k    82.29%
  1720660 requests in 10.10s, 300.29MB read
Requests/sec: 170361.31
Transfer/sec:     29.73MB
