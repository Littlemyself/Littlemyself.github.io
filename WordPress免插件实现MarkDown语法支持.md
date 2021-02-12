WordPress默认不支持MarkDown标记，商店里很多第三方MarkDown插件，但都比较复杂又太多能我不需要的功能。以前都是用HTML标签来写文章，虽然排版效果好，但是写起来效率也不高，于是想让WordPress支持MarkDown语法，并且不需要安装额外的插件。于是就网上大搜捕。还真给我找到了。

### 下载Parsedown

Parsedown可以将MarkDown内容解析为HTML，如果内容已经是HTML则不进行解析，有了Parsedown的支持，在发表WordPress文章的时候不仅兼容原来的文本模式（HTML）也可以使用MarkDown语法写作，两者互不冲突。

*   前往 [parsedown](https://github.com/erusev/parsedown/releases/) 下载最新版Parsedown
*   在主题目录下新建一个目录extend
*   将Parsedown.php放到extend目录

### 将下面的代码添加到主题目录的`functions.php`注册为WordPress钩子
```php
    //markdown解析
    function wp_parsedown(){
        include_once(get_stylesheet_directory()."/extend/Parsedown.php");
        $Parsedown = new Parsedown();

        $content = get_the_content();
        $content = $Parsedown-&gt;text($content);
        if(is_single() || is_page()){
            echo $content;
        }
        else{
            $content = strip_tags($content);
            $content = mb_substr($content,0,180,'UTF-8');
            echo $content;
        }
    }
    add_action('the_content','wp_parsedown');
```
### 添加nofollow并新窗口打开
```css
    如果文章外链需要自动添加nofollow并且在新窗口打开，请使用下面的代码：
    <pre>`//markdown解析,添加nofollow
    function wp_parsedown(){
        include_once(get_stylesheet_directory()."/extend/Parsedown.php");
        $Parsedown = new Parsedown();

        $content = get_the_content();
        $content = $Parsedown-&gt;text($content);
        if(is_single() || is_page()){
            preg_match_all('/href="(.*?)" rel="external nofollow" target = "_blank" /',$content,$matches);
             if($matches){
              foreach($matches[1] as $val){
               if( strpos($val,home_url())===false ) $content=str_replace("href=\"$val\"", 

            "href=\"$val\" rel=\"external nofollow\" target = \"_blank\" ",$content);
              }
             }

            echo $content;
        }
        else{
            $content = strip_tags($content);
            $content = mb_substr($content,0,180,'UTF-8');
            echo $content;
        }
    }
    add_action('the_content','wp_parsedown');
```
注意上面的`$content = mb_substr($content,0,180,'UTF-8');`这一行，其中180代表首页文章摘要字数，请根据自身情况修改。

### 切换到文本模式

WordPress文本模式支持HTML写作，通过上面的步骤文本模式已经完美支持了MarkDown语法。
<img src="https://qn.ymfgm.com/2021/01/snipaste_20180728_111406.png" alt="qq" title="yanshi" style="zoom:200%;" />

### 其它说明

此方法操作简单，无需安装额外的插件，完美兼容原来的文本模式。在写这篇文章的时候已经在用Markdown写作，大家可以看看效果如何。
但是使用这个方法虽然方便，但是短代码却无法使用了。本人又不会php修复不了，等待有心人。

> 本文来自：[小z博客](https://www.xiaoz.me/)有部分修改。