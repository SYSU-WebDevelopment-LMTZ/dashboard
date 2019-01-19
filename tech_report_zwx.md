# 项目心得
### by 18214687


# Python + flask 框架学习心得

## 1. 概览
flask最小的的应用：

``` 
  from flask import Flask
  app = Flask(__name__)
 
  @app.route('/')
  def hello_world():
    return 'Hello World!'
 
  if __name__ == '__main__':
      app.run()
``` 
把它保存为 hello.py，然后用 Python 解释器来运行。 确保你的应用文件名不是 flask.py ，因为这将与flask本身冲突。
运行下面代码后，访问 http://127.0.0.1:5000/就会看见 Hello World 问候。
``` 
 python hello.py
 Running on http://127.0.0.1:5000/
``` 
代码诠释：
> 首先，我们导入了 Flask 类。这个类的实例将会是WSGI 应用程序。接下来，我们创建一个该类的实例，第一个参数是应用模块或者包的名称。 如果你使用单一的模块（如本例），你应该使用 __name__ ，因为模块的名称将会因其作为单独应用启动还是作为模块导入而有不同（ 也即是 '__main__' 或实际的导入名）。这是必须的，这样 Flask 才知道到哪去找模板、静态文件等等。详情见 Flask的文档。然后，我们使用 route() 装饰器告诉 Flask 什么样的URL 能触发我们的函数。这个函数的名字也在生成 URL 时被特定的函数采用，这个函数返回我们想要显示在用户浏览器中的信息。最后我们用 run() 函数来让应用运行在本地服务器上。 其中 if __name__ =='__main__': 确保服务器只会在该脚本被 Python 解释器直接执行的时候才会运行，而不是作为模块导入的时候。欲关闭服务器，按 Ctrl+C。

## 2. 关于路由

route() 装饰器把一个函数绑定到对应的URL上，基本例子如下：
```
@app.route('/')
def index():
    return 'Index Page'

@app.route('/hello')
def hello():
    return 'Hello World'
```
除此之外，还能构造含有动态部分的 URL，也可以在一个函数上附着多个规则，这需要给URL 添加变量部分，你可以把这些特殊的字段标记为 <variable_name> ， 这个部分将会作为命名参数传递到你的函数。规则可以用 <converter:variable_name> 指定一个可选的转换器，比如int(接受整数)、float(同int，但接受浮点数)等，一些基本例子如下：
```
@app.route('/user/<username>')
def show_user_profile(username):
    # show the user profile for that user
    return 'User %s' % username

@app.route('/post/<int:post_id>')
def show_post(post_id):
    # show the post with the given id, the id is an integer
    return 'Post %d' % post_id
```

## 3. HTTP方法
HTTP 方法（也经常被叫做“谓词”）告知服务器，客户端想对请求的页面做些什么，下面是非常常见的几个方法：

> GET
    浏览器告知服务器：只 获取 页面上的信息并发给我。这是最常用的方法。

> HEAD
    浏览器告诉服务器：欲获取信息，但是只关心 消息头 。应用应像处理 GET 请求一样来处理它，但是不分发实际内容。在 Flask 中你完全无需 人工 干预，底层的 Werkzeug 库已经替你打点好了。

> POST
    浏览器告诉服务器：想在 URL 上 发布 新信息。并且，服务器必须确保 数据已存储且仅存储一次。这是 HTML 表单通常发送数据到服务器的方法。

HTTP （与 Web 应用会话的协议）有许多不同的访问 URL 方法。默认情况下，路由只回应 GET 请求，但是通过 route() 装饰器传递 methods 参数可以改变这个行为，基本例子如下。如果存在 GET ，那么也会替你自动地添加 HEAD，无需干预。它会确保遵照 HTTP RFC（描述 HTTP 协议的文档）处理 HEAD 请求，所以可以完全忽略这部分的 HTTP 规范.

```
@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        do_the_login()
    else:
        show_the_login_form()
```

