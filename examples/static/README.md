### videoJS基础使用
#### [插件地址](http://videojs.com)

#### 使用方式
1. 引入插件

```
<link href="//vjs.zencdn.net/5.11/video-js.min.css" rel="stylesheet">
<script src="//vjs.zencdn.net/5.11/video.min.js"></script>
```
2. dom元素初始化

```
<video
    id="my-player"
    class="video-js"
    controls
    preload="auto"
    poster="//vjs.zencdn.net/v/oceans.png"
    data-setup='{}'>
  <source src="//vjs.zencdn.net/v/oceans.mp4" type="video/mp4"></source>
  <source src="//vjs.zencdn.net/v/oceans.webm" type="video/webm"></source>
  <source src="//vjs.zencdn.net/v/oceans.ogv" type="video/ogg"></source>
  <p class="vjs-no-js">
    To view this video please enable JavaScript, and consider upgrading to a
    web browser that
    <a href="http://videojs.com/html5-video-support/" target="_blank">
      supports HTML5 video
    </a>
  </p>
</video>
```
3. 实例对象初始化

```
var player = videojs('my-player');
```
4.videojs方法共有三个参数，videodom对象，options选项和ready后的回调函数

```
var options = {};

var player = videojs('my-player', options, function onPlayerReady() {
  videojs.log('Your player is ready!');

  // In this context, `this` is the player that was created by Video.js.
  this.play();

  // How about an event listener?
  this.on('ended', function() {
    videojs.log('Awww...over so soon?!');
  });
});
```
#### 常用方法和事件（api实在太多，只列出常用的一下）
###### [完整api地址](http://docs.videojs.com/Player.html)
    1. autoplay()获取或者设置自动播放属性
    2. currentTime()设置或者获取当前播放进度
    3. duration()获取视屏的总长度，一般要等到视屏对象完全加载后才能获取到，一般我们会使用定时轮询的方式来获取总时长
    4. ended()获取当前视屏对象是否已经处于结束状态
    5. enterFullWindow() 当全屏不支持我们可以视频容器延伸到浏览器将让我们一样宽。经过试验改api完全无法使视屏进入全屏。分析源码后发现真正进入全屏的api应该是requestFullscreen()，但可惜该api只能又手势触发函数执行，连模拟点击都没法触发他。
    6. exitFullscreen() 退出全屏，有效的
    7. exitFullWindow() 退出全屏，试了没什么用
    8. height() 设置/获取播放器的高度
    9. width() 设置/获取播放器的宽度
    10. isFullscreen() 检查是否处于全屏模式
    11. load() 开始加载视屏
    12. loop() 在视频中获取或设置循环属性元素
    13. muted() 获取当前的静音状态
    14. pause() 暂停视频
    15. paused() 检查视屏是否暂停
    16. play() 播放视屏
    17. played() 检查视屏播放状态
    18. preload() 获取或设置预加载属性
    19. ready() 视屏对象加载完成后调用ready中的回调函数
    20. poster() 获取或设置海报图像源url
    21. reset() 重载视屏
    22. src() 更换视频源

##### 事件监听方式，采用on()监听方式，详细事件api见官方文档

```
player.on('ended', function() {
    videojs.log('Awww...over so soon?!');
  });
```
