# 知行十大小程序

前几天看到[我交知行论坛](http://zhixing.bjtu.edu.cn/portal.php)官方准备做小程序，虽然我没有固定的时间参加，但是由于职业病，也趁着开会的间隙，写个一个只展示十大的小程序玩玩，期待官方的小程序问世

```
├── server_node    后台node版
├── server_python  后台Python版
├── weichat        小程序代码，目录见下面

```

我写的这个只有简单的预览十大和图片图，没有其他功能，开发时间一小时，微信审核了三天，擦, 代码都放在[github](https://github.com/shengxinjing/zhixing_top10)，有兴趣的自取吧

![](http://oc19olbsm.bkt.clouddn.com/zhixingpreview.gif)

小程序的开发步骤就不赘述了，[官网文档](http://oc19olbsm.bkt.clouddn.com/zhixingpreview.gif)已经很详细了,大概只有这么几个步骤

* 注册小程序账号
* 系统内获取APPid
* 下载安装专门的开发者工具，并创建项目
* 编写代码（主要是js和腾讯自己造的wxml）
* 如果需要后台，需要验证一下域名，编写后端接口代码
* 预览，上传，审核，上线
* 详细步骤官网说的很详细了，不赘述了，直接看代码吧


知行是一个典型的discuz论坛，我拿不到接口权限，只能使用爬虫去爬啦，先看Python实现，web使用flask，爬虫使用request+pyquery，不清楚的看我之前的一篇[抓取知行十大博客](https://github.com/shengxinjing/my_blog/issues/5)
大概就是分别抓取热点前三，十大和轮播图的地址

![](http://oc19olbsm.bkt.clouddn.com/zhixingserver_python.jpeg)

如果你不爱python，也有nodejs版本的，web使用express，爬虫使用request+cheerio,语法基本一致

![](http://oc19olbsm.bkt.clouddn.com/zhixingserver_node.jpeg)

执行后访问地址，返回json，大概这样
![](http://oc19olbsm.bkt.clouddn.com/zhixingjson.jpg)
然后就是开发小程序啦,创建完quickstart项目后，大概文件目录这样

```
.
├── app.js    不需要改
├── app.json  配置文件 标题背景色啥的，不配也OK
├── app.wxss  样式
├── pages
│   ├── index           首页，主要写代码的地方
│   │   ├── index.js    获取数据 重要文件1
│   │   ├── index.wxml  展示   重要文件2
│   │   └── index.wxss  index页面简单的样式
│   └── logs            不需要，可以删掉的目录
│       ├── logs.js
│       ├── logs.json
│       ├── logs.wxml
│       └── logs.wxss
├── style 微信样式的css库
│   └── weui.wxss
└── utils 不需要，可以删掉的目录
    └── util.js


```

先看index.js 主要就是获取数据,腾讯自己造了一个类似react的语法，如何发送请求api见[官方文档](https://mp.weixin.qq.com/debug/wxadoc/dev/api/network-request.html#wxrequestobject)

![](http://oc19olbsm.bkt.clouddn.com/zhixingindex.jpeg)

获取完数据后，存在了页面的appdata里，可以直接展示，具体展示轮播图和列表的组件，见[官方文档](https://mp.weixin.qq.com/debug/wxadoc/dev/component/swiper.html),大概就是image显示图片，swiper显示轮播图，然后wx:for循环一下显示即可,见图

![](http://oc19olbsm.bkt.clouddn.com/zhixingwxml.jpeg)


大概就是酱紫了，最后给知行官方开发组提几个建议吧，希望官方小程序早日问世

1. 不要低估开发的难度，毕竟你们大部分都是在校学生
2. 知行现有的接口，不能支撑开发小程序，需要把所有接口转成json，你们应该需要像我一样，写个中间层，专门返回json数据的
3. 包括登录接口也是需要搞成json的
4. 我个人觉得最复杂的地方，就是具体内容的展现了，小程序是腾讯自己造的语法，只是文本还好，如果有图片，就要处理成image标签，视频音频什么的也需要转换，具体见[官方文档](https://mp.weixin.qq.com/debug/wxadoc/dev/component/audio.html#audio)






















