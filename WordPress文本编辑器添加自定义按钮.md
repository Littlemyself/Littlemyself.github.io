### 在Wordpress 亲测有效：

打开您的主题文件下的 functions.php 文件,添加以下代码！(请注意备份文件，以免误操作导致网站无法正常显示）

```php
/// 添加HTML按钮
function appthemes_add_quicktags() {
?> 
<script type="text/javascript"> 
QTags.addButton( '加粗', '加粗', '<strong>', '</strong>' );
QTags.addButton( '代码', '代码', '```css , '```' );
QTags.addButton( 'p', 'p', '<p>', '</p>' ); 
QTags.addButton( 'hr', 'hr', '<hr>', '' );
QTags.addButton( '换行', '换行', '<br/>', '' );

</script>
<?php
}
add_action('admin_print_footer_scripts', 'appthemes_add_quicktags' );
```