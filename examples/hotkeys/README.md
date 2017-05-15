### 使用videojs-hotkeys 插件为videoJS视屏添加热键功能
#### [插件地址](https://github.com/ctd1500/videojs-hotkeys)

##### 个人觉得还挺有用的一个插件，添加了键盘和视屏的交互，可以深度定制。很人性化

#### 使用方式
1. 引入插件

```
<script src="/path/to/videojs.hotkeys.js"></script>
```
2. 初始化插件

```
videojs('vidId').ready(function() {
  this.hotkeys({
    volumeStep: 0.1,
    seekStep: 5,
    enableModifiersForNumbers: false
  });
});
```
#### 配置选项和方法说明
##### 选项
1. volumeStep（十进制）：百分比增加/减少，使用向上和向下箭头键时降低音量（默认：0.1）
2. seekStep（整数）：快进和快退使用左，右箭头键时的秒数（默认值：5）
3. enableMute（布尔值）：按M键静音（默认值：true）
4. enableVolumeScroll（布尔值）：允许通过滚动鼠标滚轮增加/降低音量（默认值：true）
5. enableFullscreen（布尔）：允许切换按视频全屏通过F键（默认true）
6. enableNumbers（布尔）：允许试图通过按数字键视频（默认true）
7. enableModifiersForNumbers（布尔值）：允许使用Ctrl / Alt / Cmd + Number键在视频中跳到指定的百分比位置（默认值：true）
8. alwaysCaptureHotkeys（boolean）：使用回车键显示控制栏（默认值：false）
9. enableInactiveFocus（布尔）：控制栏小消失后点击控制栏按钮，重新获取焦点（默认：true）
10. enableJogStyle（布尔值）：上箭头和下箭头变成控制视屏快进/快退，（默认：false）

##### 方法
1.重新设置一个已有热键，下面这些已有热键可以被重新设置。

    1. playPauseKey（功能）：该功能可用于覆盖播放/暂停切换热键（默认键：空格）
    2. rewindKey（功能）：该功能可以覆盖视频中向后/向左搜索的键（默认键：左箭头）
    3. forwardKey（功能）：此功能可以覆盖在视频中寻找向前/向右的键（默认键：右箭头）
    4. volumeUpKey（功能）：此功能可以覆盖增加音量的键（默认键：向上箭头）
    5. volumeDownKey（功能）：此功能可以覆盖减小音量的键（默认键：向下箭头）
    6. muteKey（功能）：该功能可以覆盖音量静音切换键（默认键：M）
    7. fullscreenKey（功能）：此功能可以覆盖全屏切换的键（默认键：F）
###### 具体使用方式

```
  this.hotkeys({
    volumeStep: 0.1,
    fullscreenKey: function(event, player) {
      // override fullscreen to trigger when pressing the F key or Ctrl+Enter
      return ((event.which === 70) || (event.ctrlKey && event.which === 13));
    }
  });
});
//进入全屏操作添加ctrl+f键也可以进入全屏。
```
2. 创建一个新的自定义热键

```
videojs('vidId').ready(function() {
  this.hotkeys({
    volumeStep: 0.1,
    customKeys: {
      // Create custom hotkeys
      ctrldKey: {
        key: function(event) {
          // Toggle something with CTRL + D Key
          return (event.ctrlKey && event.which === 68);
        },
        handler: function(player, options, event) {
          // Using mute as an example
          if (options.enableMute) {
            player.muted(!player.muted());
          }
        }
      }
    }
  });
});
//ctrl+D静音
```
