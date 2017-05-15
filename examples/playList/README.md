### 使用videojs-playlist 插件为videoJS视屏添加多集连播功能
#### [插件地址](https://github.com/brightcove/videojs-playlist)

#### 使用方法
1. 引入插件

```
<script src="path/to/video.js/dist/video.js"></script>
<script src="path/to/videojs-playlist/dist/videojs-playlist.js"></script>
```
2. 项目初始化


```
var player = videojs('video');

player.playlist([{
  sources: [{
    src: 'http://media.w3.org/2010/05/sintel/trailer.mp4',
    type: 'video/mp4'
  }],
  poster: 'http://media.w3.org/2010/05/sintel/poster.png'
}, {
  sources: [{
    src: 'http://media.w3.org/2010/05/bunny/trailer.mp4',
    type: 'video/mp4'
  }],
  poster: 'http://media.w3.org/2010/05/bunny/poster.png'
}, {
  sources: [{
    src: 'http://vjs.zencdn.net/v/oceans.mp4',
    type: 'video/mp4'
  }],
  poster: 'http://www.videojs.com/img/poster.jpg'
}, {
  sources: [{
    src: 'http://media.w3.org/2010/05/bunny/movie.mp4',
    type: 'video/mp4'
  }],
  poster: 'http://media.w3.org/2010/05/bunny/poster.png'
}, {
  sources: [{
    src: 'http://media.w3.org/2010/05/video/movie_300.mp4',
    type: 'video/mp4'
  }],
  poster: 'http://media.w3.org/2010/05/video/poster.png'
}]);

// Play through the playlist automatically.
player.playlist.autoadvance(0);
```
#### 方法和事件
1. player.playlist([Array newList], [Number newIndex]) -> Array
 获取或设置播放器的当前播放列表。

```
player.playlist([{
  sources: [{
    src: 'http://media.w3.org/2010/05/video/movie_300.mp4',
    type: 'video/mp4'
  }],
  poster: 'http://media.w3.org/2010/05/video/poster.png'
}]);
```
第二个参数设置视频加载的index。如果省略了,默认加载第一个视屏

```
player.playlist([{
  sources: [{
    src: 'http://media.w3.org/2010/05/sintel/trailer.mp4',
    type: 'video/mp4'
  }],
  poster: 'http://media.w3.org/2010/05/sintel/poster.png'
}, {
  sources: [{
    src: 'http://media.w3.org/2010/05/bunny/trailer.mp4',
    type: 'video/mp4'
  }],
  poster: 'http://media.w3.org/2010/05/bunny/poster.png'
}], 1);
```

2. player.playlist.currentItem([Number index]) -> Number 
获取或设置当前项目索引。如果播放器正在播放非播放列表视频，它将返回-1。

```
player.currentItem();
// 0

player.currentItem(2);
// 2

player.playlist(samplePlaylist);
player.src('http://example.com/video.mp4');
player.playlist.currentItem();
// -1
```
3. player.playlist.contains(String|Object|Array value) -> Boolean 确定播放列表中是否包含字符串，源对象或播放列表项目。

```
playlist.contains('http://media.w3.org/2010/05/sintel/trailer.mp4')
// true

playlist.contains([{
  src: 'http://media.w3.org/2010/05/sintel/poster.png',
  type: 'image/png'
}])
// false

playlist.contains({
  sources: [{
    src: 'http://media.w3.org/2010/05/sintel/trailer.mp4',
    type: 'video/mp4'
  }]
});
// true
```
4. player.playlist.indexOf(String|Object|Array value) -> Number。获取播放列表中的字符串，源对象或播放列表项目的索引。如果没有找到，返回-1。

```
playlist.indexOf('http://media.w3.org/2010/05/bunny/trailer.mp4')
// 1

playlist.contains([{
  src: 'http://media.w3.org/2010/05/bunny/movie.mp4',
  type: 'video/mp4'
}])
// 3

playlist.contains({
  sources: [{
    src: 'http://media.w3.org/2010/05/video/movie_300.mp4',
    type: 'video/mp4'
  }]
});
// 4
```
5. player.playlist.first() -> Object|undefined 。播放播放列表中的第一个项目。
6. player.playlist.last() -> Object|undefined 。播放播放列表中的最后一个项目。
7. player.playlist.next() -> Object 。进入播放列表中的下一个项目。
8. player.playlist.previous() -> Object。回到播放列表中的上一个项目。
9. player.playlist.autoadvance([Number delay]) -> undefined 设置播放列表自动提前行为。一旦被调用，在播放列表中的每个视频结束时，插件将等待delay几秒钟，然后自动进入下一个视频。如果在延迟期间更改自动提前功能，则自动提前将被取消，并且不会推进下一个视频，但会为以下视频使用新的超时值。

```
// 不等待直接进入下一个视屏
player.playlist.autoadvance(0);

// 等待五秒
player.playlist.autoadvance(5);

// 重置等待时间
player.playlist.autoadvance();
```
10. player.playlist.repeat([Boolean val]) -> Boolean 当启用时，播放列表中最后一个视频之后的“下一个”视频是播放列表中的第一个视频。这会影响调用next()，自动播放等的行为。

##### 事件
1. playlistchange 每当播放列表的内容被改变时（即，当player.playlist()用参数调用时），该事件被异步地被触发

```
player.on('playlistchange', function() {
  console.log(player.playlist());
});

player.playlist([ ... ]);
// [ ... ]

player.playlist([ ... ]);
// [ ... ]
```
2. beforeplaylistitem 播放列表的内容切换之前
3. playlistitem 播放列表的内容切换时