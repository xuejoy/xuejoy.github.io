# Jmeter自定义变量及命令行执行脚本


Jmeter自定义变量、命令行执行脚本

<!--more-->

在上一篇文章 [Jmeter入门教程](https://xuexuehan.top/jmeter-base/)中介绍了Jmeter的安装及简单用法。本文主要介绍jmeter的自定义变量和使用命令行执行脚本。

### jmeter参数化

上一篇中，当http请求带有参数的时候，我们就直接在脚本中写死，但有时候我们需要给参数传不同的值来模拟用户请求，这时，就需要将**脚本与数据**分开。也就是说，我们将参数的取值封装在一个数据文件中，然后脚本去读取这个文件中参数的取值，再传递给http请求去调用。

本文我们还是以[百度](https://www.baidu.com/)接口为例，在上篇的例子上进行修改。

{{< admonition type=example title="第一步" open=true >}}

新建CSV Data Set Config，再编写数据文件（csv或txt），里面写参数的具体取值。

{{< /admonition >}}

![](https://i.loli.net/2021/04/01/aCeoREhyd8luUzg.png)

{{< admonition type=example title="第二步" open=true >}}

在CSV Data Set Config中引用刚编好的数据文件，注意引用路径最好是相对路径，并定义变量名为`search`。

{{< /admonition >}}

![](https://i.loli.net/2021/04/01/PV3z8UkfAMWFJeS.png)

{{< admonition type=example title="第三步" open=true >}}

在[百度](https://www.baidu.com/)接口中引用CSV配置文件中自定义的变量，和之前参数值写死不同的是，这次我们在`Value`值这里写成引用自定义变量的格式即`${变量名}`（${search}）。

{{< /admonition >}}

![](https://i.loli.net/2021/04/01/URqnvrCE5QMJVho.png)

现在我们就可以点击运行按钮进行执行压测了。可以在察看结果树这里看每个http请求详情，验证我们自定义参数的值是否传入http请求中。

### 命令行执行jmeter脚本

如果是要在服务器上执行jmeter脚本，那就得用命令行的形式，使用命令行的方式执行脚本，会生成两个文件：XXX.jtl（执行脚本过程中的监听结果，需要在windows的GUI界面打开察看）和XXX文件夹（存放的是之执行脚本后的测试报告）。

{{< admonition type=info  title="命令参数" open=true >}}

接下来简单介绍使用命令行执行jmeter脚本的常用参数：

- -t，--testfile：jmeter脚本存放的路径；
- -l，--logfile：生成jtl格式的测试报告；
- -n，--nongui：非界面形式运行脚本；
- -J，--jmeterproperty <argument>=<value>：自定义参数及取值；
- -e，--reportatendofloadtests：generate report dashboard after load test；
- -o，--reportoutputfolder：生成html格式测试报告的文件夹；

下来以我们这个测试[百度](https://www.baidu.com/)接口的脚本为例，试用命令行运行脚本，命令行如下：

```bash
# 进入到jmeter目录下的bin文件夹下，执行以下命令
jmeter.bat -Jparam ${search} -n -t D:\Dev\apache-jmeter-5.4.1\plan\百度.jmx -l D:\Dev\apache-jmeter-5.4.1\plan\Result.jtl -e -o D:\Dev\apache-jmeter-5.4.1\plan\Report
```

当然，我们可以把命令封装成sh脚本，最后直接执行sh脚本即可。

以上:point_up_2:
