### 使用watermark插件为videojs视屏添加水印
##### [插件地址](https://github.com/dotsub/videojs-watermark)


#### 使用说明
1. 添加css和js文件

```
<link rel="stylesheet" href="../../lib/videojs-watermark.css">
<script src="../../lib/videojs-watermark.min.js" charset="utf-8"></script>
```

2. 初始化插件

```
var player = videojs("my-video");
player.watermark({
  image:"../video/logo.png",//水印url
  position:"top-right",//水印位置共四个值，top-left, top-right, bottom-left, bottom-right，默认就是"top-right"
  fadeTime:3000,//水印每隔一段时间褪色，如果需要水印一直存在，使用null
  url:"http://www.baidu.com",//点击水印跳向的链接
});
```

#### 该插件一共只有四个配置参数
1.image://水印url

2.position://水印位置共四个值，top-left, top-right,bottom-left,bottom-right，默认就是"top-right"

3.fadeTime://水印每隔一段时间褪色，如果需要水印一直存在，使用null

4.url://点击水印跳向的链接