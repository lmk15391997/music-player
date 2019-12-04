# music-player

### 基于Vue的本地音乐播放器(适配移动端)

## 开发准备

- vscode
- vue-li脚手架
- nodejs

## 开发框架

- Css Js Html
- Vue
- Nodejs
## 上手

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

```
### 注意

> sass-loader 的版本是7.3.1 最新版本无法运行

### To-do List
- [x] 拖动选择本地音乐
- [x] 歌曲控制部分
- [x] Disk旋转效果
- [x] 歌名以及进度条显示

### Player
音乐播放器最重要的部分就是播放器了.

- 音乐解析播放使用的是Web API 中的[AudioContext](https://developer.mozilla.org/zh-CN/docs/Web/API/AudioContext) 
> 1. AudioContext接口表示由音频模块连接而成的音频处理图，每个模块对应一个AudioNode。AudioContext可以控制它所包含的节点的创建，以及音频处理、解码操作的执行。
> 2. .decodeAudioData()
AudioContext接口的decodeAudioData()方法可用于异步解码音频文件中的 ArrayBuffer. ArrayBuffer数据可以通过XMLHttpRequest和FileReader来获取. AudioBuffer是通过AudioContext采样率进行解码的,然后通过回调返回结果.
返回:一个Promise对象
> 3 .AudioContext.createBufferSource()
createBufferSource() 方法用于创建一个新的AudioBufferSourceNode接口, 该接口可以通过AudioBuffer 对象来播放音频数据
该方法返回一个AudioBufferSourceNode对象.
   >>1. AudioBufferSourceNode.buffer=目标buffer
   >>2. AudioBufferSourceNode.connect(AudioContext.destination)
   >>3. AudioBufferSourceNode.start(0)

- [FileReader](https://developer.mozilla.org/zh-CN/docs/Web/API/FileReader)  解析文件获取ArrayBuffer数据
>1. FileReader 对象允许Web应用程序异步读取存储在用户计算机上的文件（或原始数据缓冲区）的内容，使用 File 或 Blob 对象指定要读取的文件或数据。
>2. FileReader.readAsArrayBuffer()
FileReader 接口提供的 readAsArrayBuffer() 方法用于启动读取指定的 Blob 或 File 内容。当读取操作完成时，readyState 变成 DONE（已完成），并触发 loadend 事件，同时 result 属性中将包含一个 ArrayBuffer 对象以表示所读取文件的数据。

### Control 
- 播放 : 
创建一个createBufferSource()对象,往其中添加buffer,再connect至AudioContext.destination中 ,调用shart()方法

- 暂停 : 
AudioBufferSourceNode.stop(0)
AudioBufferSourceNode.disconnect(0)

- 上一首 : 
Index-- 如果Index<0 则Index=Math.max(playList.length-1,0)
- 下一首 : 
Index++ 如果Index>=playList.length Index=0

### ProgressBar
- 歌名显示 : 
marquee来滚动歌名
- 进度条显示 : 
歌曲当前位置 / 歌曲总时长  position / duration

### Disk
- 点击选取歌曲 : input file multiple  append到playerList中
- 播放旋转 : 读取保存好的transform
- 暂停旋转 : 保存当前转盘旋转的transform  window.getComputedStyle(this.$refs.cover).transform;

