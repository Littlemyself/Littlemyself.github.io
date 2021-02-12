<img src="https://qn.ymfgm.com/wp-content/uploads/2020/12/20210207224554.jpg"/>
<br/>
<video id="load_video" muted src="https://cdn.jsdelivr.net/gh/Littlemyself/grli@main/12.mp4"  style="width:100%; height:100%;" controls>
</video>

html5的`video`如果直接在文中使用可能会出现视频很小或很大的问题, 可以使用下面的方法解决

<img src="https://qn.ymfgm.com/wp-content/uploads/2021/02/20210210112432.jpeg" style="zoom:200%;" />

**代码一**，纯HTML5视频自动循环播放

```html
<!DOCTYPE HTML>
<html>
<body>
<video controls="controls" loop="loop" autoplay="autoplay" style="width:100%;vertical-align:middle;">
	<source src="movie.ogg" type="video/ogg" />
	<source src="https://cdn.jsdelivr.net/gh/Littlemyself/grli@main/12.mp4" type="video/mp4" />
</video>
</body>
</html>
```

不过火狐浏览器貌似默认禁止自动播放音频视频，需要到选项 → 隐私与安全 → 自动播放，设置允许音频和视频。

如果不设置就可以自动播放，可以使用代码二。

**代码二**，配合JS自动循环播放

```html
<!doctype html>
<html lang="en">
 <head>
  <meta charset="UTF-8">
  <title>HTML5视频自动循环播放</title>
 </head>
 <body>
	<video id="videoID" controls="controls" style="width:100%;vertical-align:middle;">
	  <source src="https://cdn.jsdelivr.net/gh/Littlemyself/grli@main/12.mp4" type="video/mp4"/>
	</video>
 </body>
<script  type="text/javascript">
window.onload = function() {
	var local1=document.getElementById('videoID');  //获取，函数执行完成后local内存释放
	local1.autoplay = true; // 自动播放
	local1.loop = true; // 循环播放
	local1.muted=true; // 关闭声音，如果为false,视频无法自动播放
	if(local1.paused){  //判断是否处于暂停状态
		local1.play();  //开启播放
	} else {
		local1.pause();  //停止播放
	}
}
function btn(){
	var local=document.getElementById('videoID');  //获取，函数执行完成后local内存释放
	if(local.paused){  //判断是否处于暂停状态
		local.play();  //开启播放
	} else {
		local.pause();  //停止播放
	}
}
</script>
</html>
```

不想显示播放控制按钮可以将`controls="controls"`删除。

代码中外链的广告视频，加载可能有点慢，换成自己的MP4视频。

其中：width:100%视频自动100%显示，vertical-align:middle用于消除视频下面的空隙。



### Video相关属性:

| 属性                                                         | 值       | 描述                                                         |                      |
| :----------------------------------------------------------- | :------- | :----------------------------------------------------------- | -------------------- |
| [autoplay](https://www.w3school.com.cn/tags/att_video_autoplay.asp) | autoplay | 如果出现该属性，则视频在就绪后马上播放。                     | autoplay="autoplay"  |
| [controls](https://www.w3school.com.cn/tags/att_video_controls.asp) | controls | 如果出现该属性，则向用户显示控件，比如播放按钮。             | controls="controls"  |
| [height](https://www.w3school.com.cn/tags/att_video_height.asp) | *pixels* | 设置视频播放器的高度。                                       | height="240"         |
| [loop](https://www.w3school.com.cn/tags/att_video_loop.asp)  | loop     | 如果出现该属性，则当媒介文件完成播放后再次开始播放。         | loop="loop"          |
| [muted](https://www.w3school.com.cn/tags/att_video_muted.asp) | muted    | 规定视频的音频输出应该被静音。                               | muted                |
| [poster](https://www.w3school.com.cn/tags/att_video_poster.asp) | *URL*    | 规定视频下载时显示的图像，或者在用户点击播放按钮前显示的图像。 | poster="/img/wl.gif" |
| [preload](https://www.w3school.com.cn/tags/att_video_preload.asp) | preload  | 如果出现该属性，则视频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。 | preload="auto"       |
| [src](https://www.w3school.com.cn/tags/att_video_src.asp)    | *url*    | 要播放的视频的 URL。                                         | src="movie.ogg"      |
| [width](https://www.w3school.com.cn/tags/att_video_width.asp) | *pixels* | 设置视频播放器的宽度。                                       | width="320"          |
| webkit-playsinline                                           |          | 在移动端使用该属性不会显示系统控制条                         | webkit-playsinline   |

### 防止视频右键另存为

```html
<script type="text/javascript">
var myVideo=document.getElementById("load_video");
$('#load_video').bind('contextmenu',function() { return false; });
</script>
```

虽然不能右键保存,但是还是会有办法保存