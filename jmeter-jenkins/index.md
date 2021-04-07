# JMeter Jenkins自动化集成


根据官方文档一步步实操在Jenkins下使用JMeter。

<!--more-->

本文按照[官方文档](https://www.jenkins.io/doc/book/using/using-jmeter-with-jenkins/)，实操如何在Jenkins下使用JMeter。

There are big advantages to use JMeter and Jenkins together. Continuous Integration and Test Automation become standards on the DevOps world, but the performance levels and system complexity are increasing day by day.

Some of the main benefits of using JMeter with Jenkins are: 

- Unattended test execution for each system
- Logs of build failures and recovery steps
- Secure and easy access to test reports of each build
- Automate routine work

当然，在集成之前，我们首先要确保电脑成功安装了JMeter和Jenkins。

### 在Jenkins上安装性能插件

<img src="https://cdn.jsdelivr.net/gh/xuejoy/picture-host/img/jenkins-plugin.png"/>

<img src="https://cdn.jsdelivr.net/gh/xuejoy/picture-host/img/jmeter-plugin.png"/>

### JMeter配置

打开你jmeter目录下的`\bin\user.properties`文件，然后在文件最后一行加入命令`jmeter.save.saveservice.output_format=xml`，并保存。该命令将帮助我们将JMeter输出集成到Jenkins中。

### 用jmeter创建测试脚本

创建完脚本，然后在终端运行以下命令：

```bash
#注意文件路径
set OUT=jmeter.save.saveservice.output_format
set JMX=jmeter-test.jmx
set JTL=jmeter-test.jtl
D:\Dev\apache-jmeter-5.4.1\bin\jmeter -j %OUT%=xml -n -t %JMX% -l %JTL%
```

运行完后，根据你自己指定的路径下会出现两个文件：

- `jmeter.save.saveservice.output_format=xml`
- `jmeter-test.jtl`

### JMeter集成到Jenkins

<img src="https://cdn.jsdelivr.net/gh/xuejoy/picture-host/img/jenkins-build.png"/>

<img src="https://cdn.jsdelivr.net/gh/xuejoy/picture-host/img/jenkins-buildnow.png"/>

<img src="https://cdn.jsdelivr.net/gh/xuejoy/picture-host/img/jenkins-success.png"/>

到此，我们就成功把jemetr集成到jenkins上了。

以上:point_up_2:


