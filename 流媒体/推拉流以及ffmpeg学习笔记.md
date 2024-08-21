在说推拉流之前先简单了解一下直播的工作原理是什么

>直播工作原理与视频转码工作原理相同，但是直播是从网络上获取直播源的视频数据之后再把处理>后的文件上传到网络中
>
>结构如下：
>
>![图片](https://github.com/w-i-sh/blog-img/blob/main/%E6%B5%81%E5%AA%92%E4%BD%93/image%20copy%2011.png?raw=true)
>
>有两个流媒体服务，但是如果直播推流和观看协议是相同的话可以使用一个流媒体服务
>
>一个流媒体服务可以被推流也可以被拉流，甚至推拉流的地址也可以是一样的
>
>流媒体服务就是视频流数据的中转站，流媒体服务会在内存中实时存储视频流的一部分数据，随着>时间的推移，数据会被循环覆盖
>
>![图片](https://github.com/w-i-sh/blog-img/blob/main/%E6%B5%81%E5%AA%92%E4%BD%93/image%20copy%2012.png?raw=true)
>由此可以把直播工作原理简化为
>![图片](https://github.com/w-i-sh/blog-img/blob/main/%E6%B5%81%E5%AA%92%E4%BD%93/image%20copy%2013.png?raw=true)
>流媒体服务的作用
>
>直播源数据一般是通过网络协议传输的，所以一般需要流媒体服务作为中转站
>
>
>
>
>直播推流场景
>
>一般场景下：
>
>需要将视频流推送到直播平台的流媒体服务上
>![图片](https://github.com/w-i-sh/blog-img/blob/main/%E6%B5%81%E5%AA%92%E4%BD%93/image%20copy%2014.png?raw=true)
>转播场景：
>
>不需要自身流媒体服务的参与接收，视频转码软件直接拉取对方的视频流即可
>![图片](https://github.com/w-i-sh/blog-img/blob/main/%E6%B5%81%E5%AA%92%E4%BD%93/image%20copy%2015.png?raw=true)
>录播场景：
>
>直播源是自己的视频文件，不需要流媒体参与接收，只需视频转码软件按照播放时间读取就行
>
>
>
>
>直播转码
>
>对视频进行加工处理
>
>如果不对视频进行转码处理并且没有安全限制，可以直接从流媒体服务中拉取视频流观看的。并且推流和观看地址是一样的。
>
>直播转码是为了一些高级功能（画中画，直播倒计时，导播，轮播，信号中断自动补帧）
>
>
>
>
>直播流数据输出
>
>对延迟要求高则使用rtmp
>![图片](https://github.com/w-i-sh/blog-img/blob/main/%E6%B5%81%E5%AA%92%E4%BD%93/image%20copy%2016.png?raw=true)
> 
>
>用户直接拉取视频流可以观看直播，但是对于带宽的占用很大，视频码率的单位和带宽的单位是一样的；视频的码率是2Mbps，服务器带宽是100Mbps，则理论上最多支持50人在线观看
>
>想要支持更多的人就需要直播CDN
>
>![图片](https://github.com/w-i-sh/blog-img/blob/main/%E6%B5%81%E5%AA%92%E4%BD%93/image%20copy%2017.png?raw=true)
>
>但是直播CDN不能提供转码功能的，如高清、流畅转换等，这就需要额外的直播转码云服务或者自己的转码软件来实现。
>
>
>
>
>参考：【【音视频处理】直播工作原理，直播CDN、推流拉流、流媒体服务究竟是什么】 https://www.bilibili.com/video/BV1fm4y117Qe/?share_source=copy_web










## 推流

将直播的内容推送至服务器的过程。

推流是指将音频、视频或其他媒体内容通过网络实时传输到服务器或在线平台，以便其他用户可以即时观看或收听的过程。在推流过程中，媒体内容会经过编码和压缩，然后通过网络传输到目标服务器。推流通常用于直播、实时视频会议、网络电视和在线游戏等应用中。




## 拉流

拉流：指服务器已有直播内容，用指定地址进行拉取的过程。

拉流是指从服务器或在线平台获取音频、视频或其他媒体内容的过程。与推流相对应，拉流是用户通过网络从服务器或在线平台请求并接收媒体内容，以便进行实时观看或收听。




## 推拉流协议
### RTMP(Real-Time Messaging Protocol)

实时信息传输协议。该协议基于TCP，是一个协议族，包括RTMP基本协议及RTMPT/RTMPS/RTMPE等多种变种。RTMP是一种设计用来进行实时数据通信的网络协议，主要用来在Flash/AIR平台和支持RTMP协议的流媒体/交互服务器之间进行音视频和数据通信。RTMP与HTTP一样，都属于TCP/IP四层模型的应用层。




每一个推流码地址唯一指向单个的直

播活动。它由<strong>rtmp://</strong>开头，包含了上传服务器地址，上传目录名和上传节点，三部分组成。所有的rtmp地址都是这种结构组成，基本同一个平台不同直播的地址前两部分是不变的。

![image](https://raw.githubusercontent.com/w-i-sh/blog-img/main/%E6%B5%81%E5%AA%92%E4%BD%93/image%20copy%2018.png)

上图所示的sreamAddress所含内容就是RTMP协议




### HLS（HTTP Live Streaming）

HLS是由苹果公司开发的一种基于HTTP的流媒体传输协议。它将媒体内容切分为小的TS（Transport Stream）片段，并通过HTTP协议进行传输。HLS广泛用于iOS和macOS设备上的流媒体播放。




### DASH（Dynamic Adaptive Streaming over HTTP）

DASH是一种基于HTTP的自适应流媒体传输协议，由MPEG组织制定。它将媒体内容切分为小的MP4片段，并通过HTTP协议进行传输。DASH可以根据网络条件和设备性能自动调整视频的码率和质量。




### WebRTC（Web Real-Time Communication）

WebRTC是一种开放的实时通信协议，支持浏览器之间的音视频传输。它使用了SRTP（Secure Real-Time Transport Protocol）和ICE（Interactive Connectivity Establishment）等协议，可以实现低延迟的点对点实时通信。




### SRT（Secure Reliable Transport）

SRT是一种安全可靠的流媒体传输协议，由Haivision开发。它通过使用前向纠错、重传机制和加密等技术，提供了高质量的流媒体传输。




## 推拉流工具ffmpeg

ffmpeg推拉流工具的安装和使用




### 推流
```
ffmpeg -re -stream_loop -1 -i  {视频文件}   -c copy -f flv {rtmp地址}
```



-re    为输入选项 ，其后没有值 ，表示按帧率读取数据(实现实时推流)

-stream_loop  -1        选项可以指定循环读取视频源的次数，-1为无限循环

-i       为输入源，其后跟着输入源的文件名及地址

-c      为输出选项 ，值为copy表示音视频的信息及编码都不改变，原封不动的copy

-f       设定输出格式




-acodec   设定声音编解码器，未设定时则使用与输入流相同的编解码器

-vcodec   设定视频编解码器，未设定时则使用与输入流相同的编解码器 

值得一说的是，有些情况下需要将视频或者流中的B帧去掉，就要将流的视频重新编码再去B帧，否则B帧是去不掉的
```
ffmpeg -re -stream_loop -1 -i yinhuatongbu.mp4 -c:a aac  -c:v libx264 -bf 0 -f rtsp {流名称}
```



### 拉流

ffplay通常作为播放器，也可以作为很多音视频数据的图形化分析工具，通过ffplay可以看到视频图像的运动方向，音频数据的波形等（用于播放等）

```
格式：ffplay [选项] ['输入文件']
```

主要选项:

'-x    width' 强制以 "width" 宽度显示

'-y    height' 强制以 "height" 高度显示

'-an'    禁止音频

'-vn'    禁止视频

'-ss pos'    跳转到指定的位置(秒)

'-t duration'    播放 "duration" 秒音/视频

'-bytes'    按字节跳转

'-nodisp'    禁止图像显示(只输出音频)

'-f fmt'    强制使用 "fmt" 格式

'-window_title title'     设置窗口标题(默认为输入文件名)

'-loop number'     循环播放 "number" 次(0将一直循环)

'-showmode mode'    设置显示模式




可选的 mode ：

'0, video' 显示视频

'1, waves' 显示音频波形

'2, rdft' 显示音频频带

默认值为 'video'，你可以在播放进行时，按 "w" 键在这几种模式间切换

'-i input_file' 指定输入文件







FFmpeg的多媒体分析器：ffprobe.exe

ffprobe是一个非常强大的多媒体分析工具，可以从媒体文件或者媒体流中获得你想要了解的媒体信息，比如音频的参数、视频的参数、媒体容器的参数信息等。（用于媒体流的分析）

格式：ffprobe [选项] [‘输入文件’]

查看流中所含帧的类型：
```
ffprobe -v quiet -select_streams v -show_entries frame=pict_type -of csv {所要检查的流}
```






















