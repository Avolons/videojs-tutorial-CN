### 使用videojs-contrib-hls插件使videojs支持hls流m3u8格式文件
#### [插件地址](https://github.com/videojs/videojs-contrib-hls/)

#### 使用说明
##### hls插件使videojs中最出名的插件，支持hls直播流。就目前直播常见的协议有三种，RTMP,RTSP,HLS。但国内大部分直播平台仍然使用flash播放器。html5播放器的直播平台几乎没有。所以是否要选择videojs来进行直播。还是一个值得好好考虑的问题。

1. 最简单的使用方式，引入hls的js文件就可以了，注意source的type属性。

```
< video  id = example-video  width = 600  height = 300  class = “ video-js vjs-default-skin ”  controls >
  < source 
     src = “ https://example.com/index.m3u8 ”
      type = “ application / x-mpegURL ” >
</ video >
< script  src = “ video.js ” > </ script >
< script  src = “ videojs-contrib-hls.min.js ” > </ script >
```
2. 如果你正在尝试使用videojs 6.0版本的话，请先加上videojs-flash插件

```
< script  src = “ https://unpkg.com/videojs-flash/dist/videojs-flash.js ” > </ script >
< script  src = “ https://unpkg.com/videojs-contrib-hls/dist/videojs-contrib-hls.js ” > </ script >
```
3. 初始化的时候也可以将选项参数传递给videojs对象

```
hls videojs（video，{html5： {
  hls ： {
    withCredentials ： true
  }
}}）;

 //或者
 
hls videojs（video，{flash： {
  hls ： {
    withCredentials ： true
  }
}}）;
```
###### 该插件的一些额外配置参数一般都是基于协议层面的选项，少有针对ui层的，在此不做过多介绍，如有需求可以自行深入该插件。