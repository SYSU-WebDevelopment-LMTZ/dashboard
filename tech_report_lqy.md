# 项目心得
### by 18214788

## 一、 项目总结

- 在这次课程项目中，由于是第一次接触软件工程项目的整个流程，所以是一步一步跟着潘老师的课程md文档走的，其中就包括了主页中文档的编写顺序及方法。
- 其中，我和zwx主要是负责的是后台，所以用例分析和建模是我们负责的，学会了用uml去构造用例图、活动图、领域模型、状态模型等，到后期还包括了架构设计，ECB顺序图和类图，特别是有次混淆了活动图和状态模型，导致状态模型画错了，好在及时发现改了过来。学会去分析这个点餐系统的各个功能是很重要的，比如，我负责的顾客用例部分，有些include和exclude的关系需要分清楚，还有就是去分析用户真正需要什么功能，将它们用图表示出来。还有就是在ECB和用例图、领域模型对应关系时，需要界定清楚什么是Boundry类、Controller类、Entity类。
- 最主要的收获是学会如何去分析和完成一个软件工程项目，还有就是各类文档的编写，包括用例分析文档、软件架构文档等。




## 二、 Python + flask 框架学习心得
## 1. 简介

flask是一个基于Python开发并且依赖jinja2模板和Werkzeug WSGI服务的一个微型框架，对于Werkzeug本质是Socket服务端，其用于接收http请求并对请求进行预处理，然后触发Flask框架，开发人员基于Flask框架提供的功能对请求进行相应的处理，并返回给用户，如果要返回给用户复杂的内容时，需要借助jinja2模板来实现对模板的处理，即：将模板和数据进行渲染，将渲染后的字符串返回给用户浏览器。

## 2. flask 概览
- 配置
> 相关配置主要放在config.py文件中，主要配置有DEBUG，数据库的连接"SQLALCHEMY_DATABASE_URI"等，还有一些可选参数DIALECT等，必须在主文件中导入这个配置文件：

``` 
  import config
  app.config.from_object(config)
``` 

- 路由
> flask的路由使用Flask应用实例的route装饰器将一个URL规则绑定到一个视图函数上。

``` 
  @app.route('/')
  def index():
      pass
  # 传参
  @app.route('/user/<username>')
  def user(username):
      pass
``` 
 

- 模型
> 一个类对应了一张表。通常会将所有模型放在一个models.py文件中，比如要建一张article表，有四个字段，分别是id,title,content，create_time，分别是四种数据类型，在models.py中定义一个Article类，如下：

``` 
  from datetime import datetime
  class Article(db.Model):
      # 设置表名
      __tablename__ = 'article'
      id = db.Column(db.Integer, primary_key=True, autoincrement=True)
      title = db.Column(db.String(30), nullable=False)
      content = db.Column(db.Text, nullable=False)
      create_time = db.Column(db.DateTime, default=datetime.now)
``` 


> 相似地，在我们的项目中model文件如下所示，定义了order类:


```
class Order(db.Model):                                                                              
    __tablename__ = 'orders'                                                                        
    id = db.Column(db.Integer, primary_key=True)                                                    
    table_id = db.Column(db.Integer, default=0)                                                     
    # customer_id = db.Column(db.Integer, db.ForeignKey('customers.id')) # 订单和顾客是多对一关系              
    restaurant_id = db.Column(db.Integer, db.ForeignKey('restaurants.id'), default=1) # 订单和餐厅是多对一关系 
    dishs = db.relationship('Dish',                                                                 
                            secondary=orderdishs,                                                   
                            backref=db.backref('orders', lazy='dynamic'),                           
                            lazy='dynamic')                                                         
    state = db.Column(db.Integer, default=0) # 0未支付 1已支付 2可取餐                                       
    price = db.Column(db.Float, nullable=False)                                                     
    note = db.Column(db.Text) # 顾客的备注                                                               
    time = db.Column(db.DateTime, default=datetime.utcnow)                                          
                                                                                                    
    def __repr__(self):                                                                             
        return '<Order id:{}\tcustomer:{}\ttime:{}>'.format(self.id, self.customer_id, self.time)                                         
```                                      

## 3. flask的基本使用（示例）
- 前两行创建一个应用程序实例。使用web服务器网关接口协议将所有从客户端接收的请求传递给这个对象处理。这个应用程序实例就是Flask类的一个对象。接下来三行代码用于注册被装饰的函数来作为一个路由。最后是启动服务程序，__name__ == '__main__'在此处使用是用于确保web服务已经启动当脚本被立即执行。一旦服务启动，它将进入循环等待请求并为之服务。这个循环持续到应用程序停止，例如通过按下Ctrl-C。有几个选项参数可以给app.run()配置web服务的操作模式。在开发期间，可以很方便的开启debug模式，将激活 debugger 和 reloader 。这样做是通过传递debug为True来实现的。


``` 
  from flask import Flask
  app = Flask(__name__)
 
  @app.route('/')
  def hello_world():
    return 'Hello World!'
 
  if __name__ == '__main__':
      app.run()
``` 


参考自：

[Python+Flask+MysqL的web建设技术过程](https://www.cnblogs.com/decadeyu/p/8145761.html)

[python web框架flask学习总结（一）](https://www.jianshu.com/p/f0db4796f949)
