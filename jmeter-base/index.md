# Jmeter入门教程


Jmeter安装与使用。

<!--more-->

### 介绍

{{< style "strong{color:#FF2700;}" >}}

The Apache JMeter™ application is open source software, a 100% pure Java application designed to **load test functional behavior and measure performance**. It was originally designed for testing Web Applications but has since expanded to other test functions.

{{< /style >}}

### 下载安装

登录[Jmeter官网](https://jmeter.apache.org/download_jmeter.cgi)下载，windows选择.zip格式下载，Linux选择.tgz格式下载。

![](https://i.loli.net/2021/03/31/QiOavI7HALb6Ud1.png)

在安装之前，首先要确保电脑已经安装了jdk1.8及以上，然后将下载的压缩包解压，然后在电脑选个路径放进去。在`\apache-jmeter-5.4.1\bin`目录下，找到`jmeter.bat`，双击就能以界面的形式启动并打开jmeter。

### Jmeter简单压测实例

比如现在我们要对[百度](https://www.baidu.com/)这个接口进行压测，主要过程如下：

{{< admonition type=example title="第一步" open=true >}}
在写测试脚本之前，我们首先要了解jmeter里面经常用到的一些基本概念。Jmeter中一个脚本即是一个测试计划，也是一个管理单元。测试计划里面的几个概念：

- 一个脚本只能出现一个测试计划；
- 一个测试计划至少要有一个**线程组**，我们可以把不相关的业务分布在不同的线程组中；
- 一个测试计划至少要有一个**取样器**，取样器其实就是我们需要测试的对象；
- 一个测试计划至少要有一个**监听器**，监听器主要用来获取测试结果，进而分析系统性能。

{{< /admonition >}}

![](https://i.loli.net/2021/03/31/iAaveyhYHk6N5G9.png)

{{< admonition type=example title="第二步" open=true >}}
了解测试计划基本概念后，我们来看下线程组里的几个概念：

- 名称和注释可以随意设置，不过最好设置成与业务相关的有意义的名称；
- 在取样器错误后执行的动作：继续（出错后会继续执行）、启动下一进程循环（出错后，则同一脚本中的余下请求不再执行，直接重新开始。比如登陆失败，则后续的操作都不可执行）、停止线程（出错后则停止当前线程，不再执行）、停止测试（如果出错则停止所有线程）、立即停止测试（出错会马上停止整个测试场景）；
- 线程属性：线程数（一个线程对应一个虚拟用户）、Ramp-Up时间（所有线程在多长时间内开始运行。若设置0秒，则开启场景后所有线程立即启动）、循环次数（请求的重复次数）；
- 调度器：脚本需要执行的时长。

{{< /admonition >}}

![](https://i.loli.net/2021/03/31/e7sZgBFXCKINOYU.png)

{{< admonition type=example title="第三步" open=true >}}
接下来就是重点，构建脚本，刚刚也提到，取样器其实就是我们要测的对象。以[百度](https://www.baidu.com/)为例：

- 在线程组里添加我们要测的http请求，配置好ip、请求方式、路径、参数等就可以进行测试了。

{{< /admonition >}}

![](https://i.loli.net/2021/03/31/mcFd3UhWMVw9o1j.png)

{{< admonition type=example title="第四步" open=true >}}

- 我们再添加下监听器，这里添加最常用的**察看结果树**和**聚合报告**，就可以来执行脚本了。

{{< /admonition >}}

{{< admonition type=example title="第五步" open=true >}}

- 点击运行按钮开始压测，并在刚添加的监听器中查看测试结果。

{{< /admonition >}}

![](https://i.loli.net/2021/03/31/zpIhlMvZtr72XnE.png)

{{< admonition type=example title="第六步" open=true >}}

就聚合报告的各项参数来看下本次压测[百度](https://www.baidu.com/)接口的结果。

- #样本：取样器运行次数总和；（这里是访问百度接口的次数）
- 平均值：请求（事务）的平均响应时间（单位：毫秒）；（请求1次百度接口需要的时间）
- 中位数：50%的请求的响应时间不超过多少毫秒；
- 90%百分比：90%的请求的响应时间不超过多少毫秒；
- 95%百分比：95%的请求的响应时间不超过多少毫秒；
- 99%百分比：99%的请求的响应时间不超过多少毫秒；
- 最小值：请求的最小响应时间（单位：毫秒）；
- 最大值：请求的最长响应时间（单位：毫秒）；
- 异常%：事务出错率；
- 吞吐量：吞吐率，即常说的TPS；（服务器每单位时间处理的请求数）
- 接收KB/sec：每秒接收的数据包流量，单位KB；
- 发送KB/sec：每秒发送的数据包流量，单位KB；

{{< /admonition >}}

![](https://i.loli.net/2021/03/31/KX7gLa5dtJv9z3W.png)

以上:point_up_2:
