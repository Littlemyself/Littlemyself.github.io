### ffmpeg 将 mp4 视频转换为 webp 格式动图

webp格式的优点我就不说了，现在iso14也支持了webp。在网站制作中我们想放一些简单的动效或动画，如果放MP4格式的视频，网页`background url(xxx.mp4);`并不支持，使用gif格式，图片太大，压缩到合适大小画面不忍直视（特短的除外）就想到了webp动图。

### 属性及特点：

1. 文件格式是 .webp
2. 无损压缩或有损压缩皆可
3. 与 JPEG 格式图片相比，WebP 格式下的有损图片能比尺寸小 25-34%
4. 与 PNG 格式图片相比，WebP 格式下的无损图片能比尺寸小 25%
5. WebP 支持无损的透明涂层，类似带 alpha channel 的 PNG 文件
6. WebP 支持动画，类似带动画的 GIF 文件 总的来说，WEBP 格式文件能够实现比 JPEG、PNG 和 GIF 更小的文件体积。

### MP4 转为 WebP 遇到的问题

基于 WebP 图片属性无需播放控制及更小的文件尺寸的考量，最近需将 MP4 格式的动画短视频转为 WebP 格式实现用于 app 中的短时动画。一开始的方法是使用在线的 Video to WebP 转换器 [ezgif](https://link.zhihu.com/?target=https%3A//ezgif.com/video-to-webp) 来转换格式。在线的可视化转换器操作上虽然方便，但却出现了以下问题： 1. ezgif 支持导出的最大webp分辨率只有 800px，难以自定义导出尺寸 2. 使用 10fps 的帧率（frame per second）导出的 webp 的视觉效果不佳 3. 使用 20fps 或更高帧率导出的 webp 图片的色彩损失严重。若画面使用较多色彩或渐变色，导出的 WebP 动画文件部分画面会出现马赛克效果，视觉体验不佳

### MP4转webp动图的几种方法

#### 第一种：多次转换

这种方法比较麻烦，先要把mp4转换成gif在把gif转换成webp动图

#### 第二种：在线转换

在线视频-webp动图转换器，例如 [OnlineConverter](https://link.zhihu.com/?target=https%3A//www.onlineconverter.com/video-to-webp) 和 [hnet](https://link.zhihu.com/?target=https%3A//hnet.com/video-to-webp/)，有些上传的视频需要保密，服务器有缓存还是有点不安全。

### 第三种方法

ffmpeg把mp4 视频转换为 webp 动图，这个方法要有一定的动手能力，有些人没开始就放弃了。

下载：[ffmpeg](http://ffmpeg.org/download.html)	进入官网按照你的系统选择以windows为例，点击windows选择[Windows builds from gyan.dev](https://www.gyan.dev/ffmpeg/builds/)	会跳转到下载页面，git和release的Links随便选一个最上面的下载即可

```html
git
Links

https://www.gyan.dev/ffmpeg/builds/ffmpeg-git-full.7z
SHA256: 2e33b40ea7dc1ee3cfcf50a89be522653a90332ce90f5dbdafdc655fdcd5fc25
https://www.gyan.dev/ffmpeg/builds/ffmpeg-git-essentials.7z
SHA256: 4fdf7f5e575126f5f786363717a427228a565e4a632fbccd2e3e28157caf22c7
```

```
release
Links

https://www.gyan.dev/ffmpeg/builds/ffmpeg-release-full.7z
SHA256: c25812b16a9000b03688a2006fdce66a890d8c86f5f5322b51db100fd7658ef4
https://www.gyan.dev/ffmpeg/builds/ffmpeg-release-essentials.7z (22MB)
SHA256: a333466265db1d4f5edd5ece32e336da27e27f25cfc73f608363b15600a7b055

https://www.gyan.dev/ffmpeg/builds/ffmpeg-release-essentials.zip (74MB)
SHA256: 68d42f9bd870e0e983b6d0827d1810d98570bac344a88a04b0bbb9ba34345920
https://www.gyan.dev/ffmpeg/builds/ffmpeg-release-full-shared.7z
SHA256: f7622eb4e21be5413cbc67b3ea0cb90369d6a4df0f64cd2c98378787e55216b3
```



<img src="https://qn.ymfgm.com/wp-content/uploads/2020/12/20210206013802.png"/>

<img src="https://qn.ymfgm.com/wp-content/uploads/2020/12/20210206013934.png"/>

下载完成解压文件得到：`ffmpeg-4.3.2-2021-02-02-full_build`的文件夹，我改名为`ffmpeg`我把ffmpeg放在D盘根目录里，随意放。

### 设置变量

在系统变量里双击选择path,选择新建，将FFmpeg的bin目录的路径D:\ffmpeg\bin加进去，如果是win7记得加上分号`;`，点击“确定”保存，即配置完成。（我放的是系统变量的Path里）

<img src="https://qn.ymfgm.com/wp-content/uploads/2020/12/20210206015235.png"/>

### 检验**ffmpeg** 是否安装成功

命令行（windows+R输入cmd）输入“ffmpeg –version”，如果出现如下说明配置成功。

```shell
sffmpeg version 4.3.2-2021-02-02-full_build-www.gyan.dev Copyright (c) 2000-2021 the FFmpeg developers
```

<img src="https://qn.ymfgm.com/wp-content/uploads/2020/12/20210206015712.png"/>

### 制作webp动图

进入图片所在文件夹复制文件路劲，打开cmd输入：` cd D:\ss`	进入视频目录。

<img src="https://qn.ymfgm.com/wp-content/uploads/2020/12/20210206020040.png"/>

以下命令行可以将名为 input.mp4 文件转化为帧率为20帧每秒，循环播放，默认渲染预设效果，分辨率为 800px宽 600px 高的无损的文件名为 output 的 .webp 文件：

```shell
ffmpeg -i input.mp4 -vcodec libwebp -filter:v fps=fps=20 -lossless 1 -loop 0 -preset default -an -vsync 0 -s 800:600 output.webp
```

若希望转出的 output.webp 动画只播放一次，有损，压缩级别为3（0-6，默认为4，越高效果越好），质量为70（0-100，默认为75，越高效果越好），越舍渲染为图片，可使用以下命令：

```shell
ffmpeg -i input.mp4 -vcodec libwebp -filter:v fps=fps=20 -lossless 0 -compression_level 3 -q:v 70 -loop 1 -preset picture -an -vsync 0 -s 800:600 output.webp
```
输入命令提示：下面的情况

```shell
File 'output.webp' already exists. Overwrite? [y/N] y
// 这个是output.webp文件名重名了，问你是不是要覆盖，覆盖：y	不覆盖：换名字
```

完成后会在视频根目录生成output.webp文件如下图：↓

![image-20210206020724996](https://qn.ymfgm.com/wp-content/uploads/2020/12/20210206020725.png)

![image-20210206020941423](https://qn.ymfgm.com/wp-content/uploads/2020/12/20210206020941.png)

### 主要选项:

将每秒帧率设为20: -filter:v fps=fps=20
设为导出为无损质量: -lossless 1
设为循环播放: -loop 0。 设为不循环播放： -loop 1
设置预设渲染模式 -preset default , 可按视频画面内容类型设置 picture, photo, text, icon, drawing 或 none。选择合适的渲染模式可导出更小的 webp 文件。 [http://ffmpeg.org/ffmpeg-all.html#Options-28](https://link.zhihu.com/?target=http%3A//ffmpeg.org/ffmpeg-all.html%23Options-28)
将导出 webp 文件分辨率设为 800px:600px： -s 800:600

以上方法也适用于其他主流视频格式导出为 webp 或 gif 动画，更多转换选项，请参考 [ffmpeg 相关文档](https://link.zhihu.com/?target=http%3A//ffmpeg.org/ffmpeg-all.html%23libwebp)。

### 完成效果：↓

**循环播放**

<img class="aligncenter" src="https://qn.ymfgm.com/wp-content/uploads/2021/tu/202154432.webp" alt="4244" />

**不循环播放**

<img class="aligncenter" src="https://qn.ymfgm.com/wp-content/uploads/2020/12/20210206021744.webp" alt="dgd" />