
---
metris文件夹中的metrics.go和metrics_version文件夹中的main.go配套使用，构成了一个简单的exporter。

其中，在metrics_version/main.go中，main函数为两个路由设置处理函数，一个是自定义的Index处理函数，另一个是Handler处理函数。然后调用metrics.Register进行注册指标。最后将两个路由绑定在5565端口。

在Index处理函数中，首先利用metrics.go设置了一个计时器，用于记录从访问该路由开始到响应的延迟，然后调用函数让metrics.go中记录请求次数的指标加一，接着获取名为"Num"的环境变量的值，调用Fibonacci函数造成一定的延时，然后再对该请求进行响应。

Handler处理函数就是将所有metrics中的指标都响应给请求。

---
在metris/metics.go文件中，首先定义指标，即请求次数、响应时延。Register函数是将指标注册到Default Registry中，其中NewAdmissionLatency函数是初始化一个计时器并返回，RequestIncrease函数将请求次数指标加一。


