### 使用videojs-contrib-ads插件为视屏添加广告功能
#### [插件地址](https://github.com/videojs/videojs-contrib-ads)

#### 使用方式
##### videojs-contrib-ads插件是一个提供了常用video.js视频广告所需要功能的库。用于减少代码的集成。这个插件看着比较复杂，其实我们完全可以按照自己的想法来实现广告功能，我个人认为最简单的方式就是在视屏上覆盖一层广告层。

##### 一旦您调用player.ads()初始化插件，它提供了六个交互点（四个事件和两个方法），您可以在集成中使用它们。（ps：这是按照官方的文档翻译的，我到现在都没明白蛰四个事件和两个方法是怎么来的，明明一堆的事件）

##### 以下是从广告插件向您整合信息的事件：

###### 1. contentupdate（EVENT） - 当新内容视频已分配给播放器时触发，意思就是当前player对象的currentsrc改变时该事件会被触发，这意味着在播放新视频时可以通过该事件获取新的广告资源
###### 2. readyforpreroll （EVENT） - 内容视频第一次播放时触发，所以可以在此触发广告资源。



##### 以下是用于向广告插件发送信息的交互点：

###### 1. adsready （EVENT） - 触发此事件，表示您的集成已准备好播放广告。
###### 2. adplaying（EVENT） - 在广告开始播放时触发此事件。如果您的整合playing在广告开始时触发事件，则会自动重新分配adplaying。
###### 3. adscanceled（EVENT） - 在启动播放器或设置新视频以完全跳过广告后触发此事件。此事件是可选的; 如果您打算展示广告，则无需担心触发它。
###### 4. adserror （EVENT） - 触发此事件，表示广告整合中出现错误，任何广告状态都会中止，以便内容恢复。
###### 5. nopreroll（EVENT） - 触发此事件，表示将不会有预卷广告。否则播放器将等待直到发生超时才能播放内容。此事件是可选的，但可以改善用户体验。
###### 6. nopostroll（EVENT） - 触发此事件表示将不会有任何后期广告。否则，如果没有后期刊物，则内容会在内容结束后触发广告事件。
###### 7. ads-ad-started （EVENT） - 每个广告开始时触发。
###### 8. contentresumed（EVENT） - 如果您的整合在广告后恢复内容时不会导致“播放”事件，请发送此事件以表明该内容可以恢复。这是添加到支持缝合广告，通常不是必需的。
###### 9. ads.startLinearAdMode()（方法） - 调用此方法来表明您的集成即将播放线性广告。该方法触发adstart由播放器发出。
###### 10. ads.endLinearAdMode()（方法） - 调用此方法来表示您的集成完成播放线性广告，准备恢复内容视频。该方法触发adend由播放器发出。
###### 11. ads.skipLinearAdMode()（方法） - 调用此方法来表示您的集成已收到广告响应，但不会播放线性广告。该方法触发adskip由播放器发出。
###### 12. ads.stitchedAds()（方法） - 获取或设置stitchedAds设置。
###### 13. ads.videoElementRecycled() （方法） - 如果content元素中发生广告回放，则返回true。

##### 您的集成可能需要包括的其他事件和属性

##### 这个项目不会发送这些事件，但是这些事件是一些惯例，使用一些您可能想要考虑发送一致性的集成。

##### 活动


```
ads-request：请求广告数据时触发。

ads-load：广告请求后可以使用广告数据时触发。

ads-pod-started：当LINEAR广告窗格启动时触发。

ads-pod-ended：LINEAR广告荚已完成时触发。

ads-allpods-completed：所有LINEAR广告完成后触发。

ads-ad-started：广告开始播放时触发。

ads-ad-ended：广告完成播放时触发。

ads-first-quartile：当广告播放头穿过第一个四分位数时触发。

ads-midpoint：当广告播放头穿过中点时触发。

ads-third-quartile当广告播放头穿过第三个四分位数时被触发。

ads-pause：广告暂停时触发。

ads-play：广告恢复后触发。

ads-mute：当广告音量已被静音时触发。

ads-click：点击广告时触发。
```


##### 属性


```
player.ads.provider = {
  "type": `String`,
  "event": `Object`
}

player.ads.ad = {
  "type": `String`,
  "index": `Number`,
  "id": `String`,
  "duration": `Number`,
  "currentTime": `Function`
}
```
##### 宏（个人感觉作用不大，还不太好用）

###### 广告库的可选功能——广告宏。广告集成通常会使用广告宏，支将运行时将值添加到服务器URL或配置中。

##### 例如，支持此功能的广告集成可能会接受如下所示的广告服务器网址：


```
'http://example.com/vmap.xml?id={player.id}'
```


###### 在广告集成中，它将使用videojs-contrib-ads宏功能来处理该网址，如下所示：


```
serverUrl = player.ads.adMacroReplacement(serverUrl, true, additionalMacros);
```


###### 这将导致如下所示的服务器URL：


```
'http://example.com/vmap.xml?id=12345'
```


###### 其中12345是播放器ID。

###### adMacroReplacement需要3个参数：

1. 具有要替换的宏的字符串。
2. true如果宏值在插入时应该是URI编码的，否则false（默认false）
3. 定义其他宏的可选对象，如{'{five}': 5}（默认{}）


名称 | 值
---|---
{player.id}	| The player ID
{player.duration} 	| 	The duration of current video*
{timestamp}		| Current epoch time
{document.referrer}	| 	Value of document.referrer
{window.location.href}	| 	Value of window.location.href
{random}	| 	A random number 0-1 trillion
{mediainfo.id}	| 	Pulled from mediainfo object
{mediainfo.name}	| 	Pulled from mediainfo object
{mediainfo.description}		| Pulled from mediainfo object
{mediainfo.tags}	| 	Pulled from mediainfo object
{mediainfo.reference_id}	| 	Pulled from mediainfo object
{mediainfo.duration}	| 	Pulled from mediainfo object
{mediainfo.ad_keys}		| Pulled from mediainfo object

###### 再往下的内容如果有兴趣的可以自己看，太多了，而且总感觉这个插件的好多功能用途不广。示例中展示了一个简单的广告集成例子，实际上的肯定会复杂的多