# 随机图片签名档
顾名思义，这些代码可以随机显示图片，可以用于论坛站点的随机签名档图片。

## 功能
* 随机显示图片
* 整点报时

## 使用方法
### 工具/材料
* 文本编辑工具
* 一台服务器/主机或云函数托管（重要）

### 配置参数
#### 基本图片参数
首先打开index.php，我们可以看到这样的代码：
```
  	$sg[1]=""; 
	$sg[2]=""; 
	$sg[3]=""; 
```
其中，变量$sg[]用于存放图片地址。例如我们要把
* www.example.com/image1.png
* www.example.com/image2.png
* www.example.com/image3.png
放入随机图片列表：
```
  	$sg[1]="http://www.example.com/image1.png"; 
	$sg[2]="http://www.example.com/image2.png"; 
	$sg[3]="http://www.example.com/image3.png"; 
```
这样，我们便完成了随机图片的配置。

#### 报时图片参数
如果你不希望使用这项功能，您可以将以下代码删除：
```
 	if (date("i")=="00") {
 		$out="1".date("H")."00";
		header("location:$sg[$out]"); 
	} else { ... }
```
保留：
```
	$out=rand(1, <随机范围>);
	header("location:$sg[$out]"); 
```

此处配置图片地址同上一节，但不同的是这些图片存放站$sg[]数组的特定位置，规则如下：
* 1 + <时(前导零)> + 00
例如，早上9点的报时图片，对于的数组序号是10900.

#### 最后的一些配置
千万不要忘记这一步，可能你刚才已经注意到了，光是插入图片地址还没完事，因为最后会生成一个随机数来决定跳转到哪个图片。如果随机数范围指定不正确会发生很麻烦的事情。我们可以在末尾找到这样的一行代码：
```
  	$out=rand(1, 3);
```
此处限定了随机数范围在1~3内。你插入了多少张图片，就输入多大的范围。哦对了，回去检查一下你有没有输入重复的数组编号。

### 上传文件到服务器
保存好文件后，我们把文件上传到服务器就OK了。需要注意的是，如果服务器里已经存在index.php，那么请修改该文件名称，这不会有任何影响。

### 调用
例如，你把文件上传到了www.example.com/index.php

#### HTML
```
<img src="http://www.example.com/index.php" />
```
#### BBCode
```
[img]http://www.example.com/index.php[/img]
```

### 拓展
#### 个性化URL地址
使用.htaccess文件自定义URL地址。不同的服务器系统可能有不同的定义方法，以下代码仅供参考。
```
RewriteCond %{QUERY_STRING} ^(.*)$
RewriteRule ^自定义地址$ index.php
```

## 更新日志
* 2019/10/08 上传了本体文件。
