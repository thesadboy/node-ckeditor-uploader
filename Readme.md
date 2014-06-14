###NODE CKEDITOR UPLOADER

tulayang
itulayangi@gmail.com

2014-6-14

Ckeditor是一个不错的在线编辑器，但是却不提供上传元素.
node_ckeditor_uploader.js是一个为Ckeditor添加上传控件的扩展代码, 添加了向服务器提交图片的功能, 并保持了Ckeditor原程序的图片处理功能.

####屏幕截图

![screenshot](http://d2.freep.cn/3tb_140614203123qmef533354.png)

![screenshot](http://d2.freep.cn/3tb_140614203123al07533354.png)

![screenshot](http://d3.freep.cn/3tb_140614203123ln1a533354.png)

![screenshot](http://d3.freep.cn/3tb_1406142031231dpc533354.png)

![screenshot](http://d2.freep.cn/3tb_140614203124xfvu533354.png)

![screenshot](http://d3.freep.cn/3tb_140614203124e07n533354.png)

####如何使用

1.官网下载CKEDITOR http://ckeditor.com/download

2.导入文件

```<script src="http://127.0.0.1:8800/js/ckeditor/ckeditor.js"></script>```
```<script src="http://127.0.0.1:8800/js/node_ckeditor_uploader.js"></script>```

3.配置

* html模板
`<form id="new-blog-form" data-image-action="/{{username}}/image/new" action="/{{username}}/blog/new" method="post">
    <input name="title" placeholder="标题"/>
    <textarea name="text" class="ckeditor"></textarea>
    <button>发布</button>
</form>`

* 后端
`res.end('<div id="ckeditor_src" data-src="http://127.0.0.1:8800/images/lili/0f72277c698b97476c98e15f8c4665bd.jpg"></div>');`

* 前端配置
`
window.addEventListener('load', function () {
    CKEDITOR.extendCKEDITOR({
        actionUrl: document.getElementById('new-blog-form').getAttribute('data-image-action'),
        responseId: 'ckeditor_src',
        responseAttr: 'data-src'
    }, 'ckeditor_src', 'data-src');
    //CKEDITOR.replace('text');
}, false);`

当点击“浏览文件...”按钮的时候，自动触发change事件，并向服务器上传文件.

* actionUrl 上传文件的服务器路由，nodejs服务器应该对actionUrl路由提供保存文件，返回保存的文件路径.
返回的文件路径应该保存一个div元素的data-src属性中，并设置id.

* responseId 服务器响应返回的div元素的id

* responseAttr 服务器响应返回的div元素中的自定义属性, 携带上传文件路径
