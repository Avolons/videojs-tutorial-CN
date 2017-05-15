### 使用videojs-resolution-switcher插件为视屏添加清晰度切换
#### [插件地址](https://github.com/kmoskwiak/videojs-resolution-switcher)

#### 使用说明
1.引用js和css文件

```
<link rel="stylesheet" href="../../lib/videojs-resolution-switcher.css">
<script src="../../lib/videojs-resolution-switcher.js" charset="utf-8"></script>
```
2.初始化项目

```
videojs('my-video', {
            controls: true,
            plugins: {
                videoJsResolutionSwitcher: {
                    default: 'low',
                    dynamicLabel: true
                }
            }
        }, function() {
            var player = this;
            window.player = player;
            /*此处放置视屏数据，格式为数组，下面有被注释的示例*/
            player.updateSrc(
                [{
                        src: '../video/example.m4v',
                        type: 'video/mp4',
                        label: '标清',
                        res: 360
                    }, {
                        src: '../video/example.m4v',
                        type: 'video/mp4',
                        label: '高清',
                        res: 720
                    },
                    {
                        src: '../video/example.m4v',
                        type: 'video/mp4',
                        label: '超清',
                        res: 1080
                    }
                ]
            );
        })
```

#### 配置参数和方法说明
##### 参数
1. default://默认分辨率 使用"low"或者"high" 系统会自动选择最低或者最高的分辨率，也可以手动指定分辨率，使用res属性作为参数，例如在当前例子中，我设置‘default：360’，则分辨率默认为标清。
2. dynamicLabel://是否显示分辨率图标，默认显示，设置为false则不显示。
3. customSourcePicker://自定义函数，筛选当前所有资源。
4. ui：//完全不知道有啥用，api上说的是设置为false则按钮不显示，但是我并没有找到是哪个按钮。所以这个属性不用管。


##### 方法
1. updateSrc([source])：和videojs的src(),方法类似，用于载入资源。
2. currentResolution([label], [customSourcePicker])：返回指定的视频和清晰度。


```
// 返回当前资源
player.currentResolution(); // returns object {label '', sources: []}

// 设置资源
player.currentResolution('高清'); // returns videojs player object
```
该方法接受两个参数，
1. label：//清晰度
2. customSourcePicker：//自定义筛选函数，用于当资源不止一个时，进行资源筛选。和vjs-playlist插件配合使用时可能有用。该插件有三个参数。
    1. player
    2. sources
    3. label

```
player.currentResolution('SD', function(_player, _sources, _label){
  return _player.src(_sources[0]); \\ Always select first source in array
});
```
3. getGroupedSrc()://按照资源类型，分辨率，清晰度返回资源分组。