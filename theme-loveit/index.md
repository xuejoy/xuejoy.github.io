# 搭建Hugo博客并部署到Github


利用Hugo框架搭建个人博客

<!--more-->

{{< admonition type=note title="初衷" open=true >}}

毕业工作也有大半年了，最近一阵子发现，我已经好久没有学习新的技术，而且对什么事情都是三分热度，再这样下去怕是要废了:joy:

去年可能是因为疫情原因，在家里躺的太久，整个人有点丧:sleepy:，做啥事都提不起兴趣。工作后，发现周围的人都很优秀，莫名陷入一种焦虑的情绪中，加上抖音经常推送的一些内容，使我有点浮躁。

我觉得人还是需要给自己设定目标，这样才会有动力激发自己的潜能:dancer:

现在突然想搭建个博客，用于记录工作学习中踩的坑，或是学习总结，或是日常记录...不管怎样，都要坚持更新下去，算是今年给自己立的一个flag吧:thinking:

废话不多说，第一篇博客就记录下搭建Hugo博客的过程吧。

{{< /admonition >}}

{{< music url="/music/永不失联的爱.mp3" name=永不失联的爱 artist=米卡 cover="/images/永不失联的爱.jpg" >}}

### 安装Hugo

{{< admonition type=info title="Hugo介绍" open=true >}}
我之前用过Hexo搭建个人博客，选择Hexo搭建个人博客也是个不错的选择，但就是内容多的时候，每次生成静态资源的速度有点慢。所以这次我就选了Hugo来搭建个人博客，最主要的原因还是因为这个框架是**基于go语言**开发的，因此它最大的优势就是**速度快，效率高**:wink:
{{< /admonition >}}

Hugo安装很简单，在[官网](https://github.com/gohugoio/hugo/releases )下载所需的安装包，建议直接安装hugo_extended版本，因为LoveIt主题中有一些Features的实现只有extended版本的Hugo支持。

```bash
snap install hugo --channel=extended
```

安装完后，检查安装是否成功：

```bash
hugo version
```

接着，我们来创建博客的站点：

```bash
hugo new site myblog  #myblog是你创建站点的名称
```

### 安装主题

{{< admonition type=tip title="LoveIt：A Clean, Elegant but Advanced Hugo Theme" open=true >}}

在[Hugo主题](https://themes.gohugo.io/)官网上有很多不同风格的主题可供选择，这里我安装的是LoveIt这款主题。

{{< /admonition >}}

进入刚创建的博客站点路径，下载LoveIt主题：

```bash
git clone https://github.com/dillonzq/LoveIt.git themes/LoveIt
```

#### 主题配置

这里很容易出错，我在配置的时候，一直在报错，后面才发现原来是我的操作不对:dizzy_face:

{{< admonition type=warning  title="一定注意" open=true >}}

将LoveIt提供的**范例站点文件直接覆盖当前站点**。

```bash
cp themes/LoveIt/exampleSite/* .
```

并且如果不能访问Instagram网站，还需要删除`content/posts/theme-documentation-built-in-shortcodes`文件夹，否则会报错。

修改config.toml：关闭获取git信息，注释掉主题目录。

```bash
# 是否使用 git 信息
enableGitInfo = false
# 主题目录
# themesDir = "../.."
```

{{< /admonition >}}

配置完主题，我们可以新增一篇博客并预览下效果：

```bash
# 新增博文
hugo new posts/first.md
# 预览效果
hugo serve
```

我们通过修改**config.toml**文件，可以自定义配置博客站点的信息，真正实现个人博客的自定义化。

具体参数可以参考:point_right:[官网](https://hugoloveit.com/zh-cn/)。

### 部署到Github

{{< admonition type=success title="部署到github上，可以通过公网访问个人博客" open=true >}}

至此，我们已经搭建完个人博客的站点了，那问题来了，如果别人想访问或者自己通过公网怎么才能访问刚刚搭建的博客呢？接下来我们只需要将博客部署到Github上，就可以通过链接直接访问我们的博客了。

{{< /admonition >}}

首先在GitHub上创建一个Repository，命名为：xxx.github.io （xxx就是你的github用户名的小写）；

将我们博客的静态资源编译打包：

```bash
hugo  --baseUrl="https://xxx.github.io" --buildDrafts
```

可以看到博客根目录下多了个`public`的文件夹，该文件夹的内容就是Hugo生成的整个静态网站内容。接着，只需要进入`public`文件夹下执行我们熟悉的git提交代码命令，即可通过`https://xxx.github.io`链接访问个人博客。

```bash
cd public
git init
git add *
git commit -m "第一次提交"
git remote add origin https://github.com/xxx/xxx.github.io.git
git push -u origin master
```

以上:point_up_2:，我们的个人博客站点就搭建完成了。


