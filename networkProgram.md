### 1.TIME_WAIT状态过多的解决办法
通常通过调整内核参数解决该类问题，这里涉及到两个重要参数： https://blog.csdn.net/twt936457991/article/details/90574284
* tcp_tw_recycle：尽快回收处于TIME_WAIT状态的连接
* tcp_tw_reuse：复用处于TIME_WAIT状态的连接
* tcp_max_tw_buckets： https://www.jianshu.com/p/b7e991be0909 
允许TIME_WAIT的连接的最大数量，大于这个值新的time_wait状态将会无法创建，当前连接会消失，对端服务器会收到一个reset包，该方式违反TCP/IP协议。所以该数值应当尽量调大
* tcp_fin_timeout：该参数调整连接处于FIN_WAIT2的时间，<span style="color:red">这个地方还不太理解</span>