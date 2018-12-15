# 7.3 API 设计

## 一、API列表

### 1.1 餐厅帐号

功能|URL
-|-
[注册餐厅账户](#2.1.1)|/restaurant
[登陆餐厅账户](#2.1.2)|/restaurant/session
[退出餐厅账户](#2.1.3)|/restaurant/session
[获取餐厅信息](#2.1.4)|/restaurant/self/info
[修改餐厅信息](#2.1.5)|/restaurant/self/info

### 1.2 菜品

功能|URL
-|-
[查看所有菜品](#2.2.1)|/dishs
[获取菜品详细信息](#2.2.2)|/dish/:id
[添加菜品](#2.2.3)|/dish/:id
[编辑菜品详细信息](#2.2.4)|/dish/:id
[删除菜品](#2.2.5)|/dish/:id
[查看推荐菜品](#2.2.6)|/recommendation
[添加推荐菜品](#2.2.7)|/recommendation
[删除推荐菜品](#2.2.8)|/recommendation

### 1.3 订单

功能|URL
-|-
[查看所有订单](#2.3.1)|/orders
[获取订单详细信息](#2.3.2)|/order/:id/info
[支付订单](#2.3.3)|/order/:id/payment
[提交订单](#2.3.4)|/order
[处理订单](#2.3.5)|/order/:id

## 二、API细节

### 2.1 餐厅帐号

#### <span id="2.1.1">2.1.1 注册餐厅账户</span>
- **接口地址：** /restaurant
- **请求方法：** POST
- **接口参数：**
    ```
    {
        "phone" : "string",
        "password" : "string",
        "logo" : "string",
        "description" : "string"
    }
    ```
- **接口返回值：**
    - 200
    - 400
        ```
        {
            "message" : "string"
        }
        ```

#### <span id="2.1.2">2.1.2 登陆餐厅账户</span>
- **接口地址：** /restaurant/session
- **请求方法：** POST
- **接口参数：**
    ```
    {
        "phone" : "string",
        "password" : "string"
    }
    ```
- **接口返回值：**
    - 200
    - 400
        ```
        {
            "message" : "string"
        }
        ```

#### <span id="2.1.3">2.1.3 退出餐厅账户</span>
- **接口地址：** /restaurant/session
- **请求方法：** DELETE
- **接口参数：**
- **接口返回值：**
    - 200
    - 400
        ```
        {
            "message" : "string"
        }
        ```

#### <span id="2.1.4">2.1.4 获取餐厅信息</span>
- **接口地址：** /restaurant/self/info
- **请求方法：** GET
- **接口参数：**
- **接口返回值：**
    - 200
        ```
        {
            "phone" : "string",
            "password" : "string",
            "logo" : "string",
            "description" : "string"
        }
        ```
    - 400
        ```
        {
            "message" : "string"
        }
        ```

#### <span id="2.1.5">2.1.5 修改餐厅信息</span>
- **接口地址：** /restaurant/self/info
- **请求方法：** POST
- **接口参数：**
    ```
    {
        "phone" : "string",
        "password" : "string",
        "logo" : "string",
        "description" : "string"
    }
    ```
- **接口返回值：**
    - 200
    - 400
        ```
        {
            "message" : "string"
        }
        ```

### 2.2 菜品

#### <span id="2.2.1">2.2.1 查看所有菜品</span>
- **接口地址：** /dishs
- **请求方法：** GET
- **接口参数：**
- **接口返回值：**
    - 200
        ```
        [
            {
                "dishid" : 0
                "name" : "string"
                "price" : 0
                "imageurl" : "string"
            }
        ]
        ```
    - 400
        ```
        {
            "message" : "string"
        }
        ```

#### <span id="2.2.2">2.2.2 获取菜品详细信息</span>
- **接口地址：** /dishs/:id
- **请求方法：** GET
- **接口参数：**
- **接口返回值：**
    - 200
        ```
        {
            "dishid" : 0
            "name" : "string"
            "price" : 0
            "description" : "string"
            "imageurl" : "string"
        }
        ```
    - 400
        ```
        {
            "message" : "string"
        }
        ```

#### <span id="2.2.3">2.2.3 添加菜品</span>
- **接口地址：** /dishs/:id
- **请求方法：** POST
- **接口参数：**
    ```
    {
        "dishid" : 0
        "name" : "string"
        "price" : 0
        "description" : "string"
        "imageurl" : "string"   
    }
    ```
- **接口返回值：**
    - 200
    - 400
        ```
        {
            "message" : "string"
        }
        ```

#### <span id="2.2.4">2.2.4 编辑菜品详细信息</span>
- **接口地址：** /dishs/:id
- **请求方法：** PUT
- **接口参数：**
    ```
    {
        "dishid" : 0
        "name" : "string"
        "price" : 0
        "description" : "string"
        "imageurl" : "string"   
    }
    ```
- **接口返回值：**
    - 200
    - 400
        ```
        {
            "message" : "string"
        }
        ```

#### <span id="2.2.5">2.2.5 删除菜品</span>
- **接口地址：** /dishs/:id
- **请求方法：** DELETE
- **接口参数：**
- **接口返回值：**
    - 200
    - 400
        ```
        {
            "message" : "string"
        }
        ```

#### <span id="2.2.6">2.2.6 查看推荐菜品</span>
- **接口地址：** /recommendation
- **请求方法：** GET
- **接口参数：**
- **接口返回值：**
    - 200
        ```
        {
            "recommendationid" : 0
            "dishid" : 0
            "description" : "string"
        }
        ```
    - 400
        ```
        {
            "message" : "string"
        }
        ```

#### <span id="2.2.7">2.2.7 添加推荐菜品</span>
- **接口地址：** /recommendation
- **请求方法：** POST
- **接口参数：**
    ```
    {
        "dishid" : 0 
    }
    ```
- **接口返回值：**
    - 200
    - 400
        ```
        {
            "message" : "string"
        }
        ```

#### <span id="2.2.8">2.2.8 删除推荐菜品</span>
- **接口地址：** /recommendation
- **请求方法：** DELETE
- **接口参数：**
    ```
    {
        "dishid" : 0 
    }
    ```
- **接口返回值：**
    - 200
    - 400
        ```
        {
            "message" : "string"
        }
        ```

### 2.3 订单

#### <span id="2.3.1">2.3.1 查看所有订单</span>
- **接口地址：** /orders
- **请求方法：** GET
- **接口参数：**
- **接口返回值：**
    - 200
        ```
        [
            {
                "orderid" : 0
                "tableid" : 0
                "state" : "string"
                "price" : 0
                "ordertime" : "string"
            }
        ]
        ```
    - 400
        ```
        {
            "message" : "string"
        }
        ```

#### <span id="2.3.2">2.3.2 获取订单详细信息</span>
- **接口地址：** /order/:id/info
- **请求方法：** GET
- **接口参数：**
- **接口返回值：**
    - 200
        ```
        {
            "orderid" : 0
            "tableid" : 0
            "state" : "string"
            "price" : 0
            "ordertime" : "string"
            "dishid" : [0]
            "note" : "string"
        }
        ```
    - 400
        ```
        {
            "message" : "string"
        }
        ```

#### <span id="2.3.3">2.3.3 支付订单</span>
- **接口地址：** /order/:id/payment
- **请求方法：** POST
- **接口参数：**
    ```
    {
        "price" : 0
    }
    ```
- **接口返回值：**
    - 200
    - 400
        ```
        {
            "message" : "string"
        }
        ```

#### <span id="2.3.4">2.3.4 提交订单</span>
- **接口地址：** /order
- **请求方法：** POST
- **接口参数：**
    ```
    {
        "orderid" : 0
        "tableid" : 0
        "state" : "string"
        "price" : 0
        "ordertime" : "string"
        "dishid" : [0]
        "note" : "string"
    }
    ```
- **接口返回值：**
    - 200
    - 400
        ```
        {
            "message" : "string"
        }
        ```

#### <span id="2.3.5">2.3.5 处理订单</span>
- **接口地址：** /order/:id
- **请求方法：** POST
- **接口参数：**
    ```
    {
        "receive" : true
    }
    ```
- **接口返回值：**
    - 200
    - 400
        ```
        {
            "message" : "string"
        }
        ```