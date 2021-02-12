给网站登录添加验证码功能在一定程度上可以有效减少机器人软件暴力破解暴力登录，对于wordpress程序可以有很多相关插件可以实现，不过这么简单的功能其实没有必要安装一个插件，通过简单的代码也很容易实现。

#### 把下面的代码添加到当前主题的functions.php文件：

```php
function login_val_fields() {
  
//获取两个随机数, 范围0~9
  $num1 = rand(0,9);
  $num2 = rand(0,9);
  echo "<p><label for='math' class='small'>验证码</label> $num1 + $num2 = ?<input type='text' name='sum' class='input' value='' size='25' tabindex='4'>"."<input type='hidden' name='num1' value='$num1'>"."<input type='hidden' name='num2' value='$num2'></p>";
}
add_action('login_form','login_val_fields');
 
function login_val() {
  if(isset($_POST['sum'])){
    
//获取用户提交的计算结果
    $sum=$_POST['sum'];
    switch($sum){
	
//得到正确的计算结果则直接跳出
	case $_POST['num1']+$_POST['num2']:
        break;
	
//未填写结果时的错误讯息
	case null:
           wp_die('错误: 请输入验证码.');
	break;
	
//计算错误时的错误讯息
	default:
           wp_die('错误: 验证码错误,请重试.');
    }
  }
}
add_action('login_form_login','login_val');
```

