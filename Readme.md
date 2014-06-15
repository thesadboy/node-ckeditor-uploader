Node Ckeditor Uploader

tulayang  
itulayangi@gmail.com

2014-6-14

Ckeditor是一个不错的在线编辑器，但是却不提供上传元素. 

node_ckeditor_uploader.js是一个为Ckeditor添加上传控件的扩展代码, 添加了向服务器提交图片的功能, 并保持了Ckeditor原程序的图片处理功能.

node_ckeditor_uploader.js扩展了“dialogDefinition”对话框渲染事件，其他的配置仍然遵循官网方式.

##屏幕截图

![screenshot](http://d2.freep.cn/3tb_140614203123qmef533354.png)

![screenshot](http://d2.freep.cn/3tb_140614203123al07533354.png)

![screenshot](http://d3.freep.cn/3tb_140614203123ln1a533354.png)

![screenshot](http://d3.freep.cn/3tb_1406142031231dpc533354.png)

![screenshot](http://d2.freep.cn/3tb_140614203124xfvu533354.png)

![screenshot](http://d3.freep.cn/3tb_140614203124e07n533354.png)

##如何使用

官网下载CKEDITOR http://ckeditor.com/download

####配置html模板
```sh
// 最重要的是"textarea"元素
// 设置class=ckeditor, CKEDITOR会自动为其渲染编辑器形状
<form id="new-blog-form" data-image-action="/{{username}}/image/new" action="/{{username}}/blog/new" method="post">
    <input name="title" placeholder="标题"/>
    <textarea name="text" class="ckeditor"></textarea>1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
Node Ckeditor Uploader
tulayang  
itulayangi@gmail.com
2014-6-14
Ckeditor是一个不错的在线编辑器，但是却不提供上传元素. 
node_ckeditor_uploader.js是一个为Ckeditor添加上传控件的扩展代码, 添加了向服务器提交图片的功能, 并保持了Ckeditor原程序的图片处理功能.
node_ckeditor_uploader.js扩展了“dialogDefinition”对话框渲染事件，其他的配置仍然遵循官网方式.
##屏幕截图
![screenshot](http://d2.freep.cn/3tb_140614203123qmef533354.png)
![screenshot](http://d2.freep.cn/3tb_140614203123al07533354.png)
![screenshot](http://d3.freep.cn/3tb_140614203123ln1a533354.png)
![screenshot](http://d3.freep.cn/3tb_1406142031231dpc533354.png)
![screenshot](http://d2.freep.cn/3tb_140614203124xfvu533354.png)
![screenshot](http://d3.freep.cn/3tb_140614203124e07n533354.png)
##如何使用
官网下载CKEDITOR http://ckeditor.com/download
####配置html模板
```sh
// 最重要的是"textarea"元素
// 设置class=ckeditor, CKEDITOR会自动为其渲染编辑器形状
<form id="new-blog-form" data-image-action="/{{username}}/image/new" action="/{{username}}/blog/new" method="post">
    <input name="title" placeholder="标题"/>
    <textarea name="text" class="ckeditor"></textarea>
    <button>发布</button>
</form>
```
####配置服务器端
```sh
// 收到请求, 保存图片
// ...
// 返回响应，传送已保存图片的路径
var id = 'ckeditor_src';
wt
Commit changes

    <button>发布</button>
</form>
```

####配置服务器端
```sh
// 收到请求, 保存图片
// ...
// 返回响应，传送已保存图片的路径
var id = 'ckeditor_src';
var data_src = 'http://127.0.0.1:8800/images/lili/0f72277c698b97476c98e15f8c4665bd.jpg'
res.end('<div id=' + id + 'data-src=' + data_src + '></div>');
```

####配置前端

```sh
<script src="http://127.0.0.1:8800/js/ckeditor/ckeditor.js"></script>
```
```sh
<script src="http://127.0.0.1:8800/js/node_ckeditor_uploader.js"></script>
```
```sh
window.addEventListener('load', function () {
    CKEDITOR.extendCKEDITOR({
        actionUrl: document.getElementById('new-blog-form').getAttribute('data-image-action'),
        responseId: 'ckeditor_src',
        responseAttr: 'data-src'
    });
}, false);
```
##逻辑流程
当点击``浏览文件...``按钮的时候，自动触发change事件，并向服务器上传文件. 
服务器接受传送的请求体，保存图片，并把保存后的图片路径，挂到div元素上，发回客户端.
编辑器接受响应后，自动设置URL为图片路径，应用编辑器内核图片处理功能.

####CKEDITOR.extendCKEDITOR函数的参数配置
* actionUrl 上传文件的服务器路由，nodejs服务器应该对actionUrl路由提供保存文件，返回保存的文件路径.
返回的文件路径应该保存一个div元素的data-src属性中，并设置id.

* responseId 服务器响应返回的div元素的id

* responseAttr 服务器响应返回的div元素中的自定义属性, 携带上传文件路径
