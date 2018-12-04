# 8.2 REST API设计规范

### 一、接口编码
- 接口请求参数和响应数据均使用utf-8编码
- 请求头指定内容及编码类型
    ```
    Content-Type: text/html; charset=UTF-8
    或
    Content-Type: application/json; charset=UTF-8
    ```

### 二、接口协议
- 使用更安全的HTTPS协议进行数据传输

### 三、返回数据格式
- 接口返回数据使用Json格式

### 四、返回码
#### 1 HTTP状态码
- 服务器向用户返回的状态码和提示信息，常见的有以下一些：
    - 200 OK - [GET]：服务器成功返回用户请求的数据，该操作是幂等的（Idempotent）
    - 400 INVALID REQUEST - [POST/PUT/PATCH]：用户发出的请求有错误，服务器没有进行新建或修改数据的操作，该操作是幂等的
    - 401 Unauthorized - [*]：表示用户没有权限（令牌、用户名、密码错误）
    - 403 Forbidden - [*] 表示用户得到授权（与401错误相对），但是访问是被禁止的
    - 404 NOT FOUND - [*]：用户发出的请求针对的是不存在的记录，服务器没有进行操作，该操作是幂等的
    - 500 INTERNAL SERVER ERROR - [*]：服务器发生错误，用户将无法判断发出的请求是否成功

#### 2 业务状态码
- 服务器通过业务状态码向用户返回请求状态和提示信息
- 业务状态码需进行统一管理，同一项目必需保证业务状态码具有唯一性

### 五、返回数据
- 请求成功时直接返回业务数据，失败时返回错误码和提示信息
- 示例如下
    - 获取指定用户的信息
        ```
        GET /v1/users/45701
        ```
    - 成功时返回
        ```
            {
            "nickname":"张三",
            "nation_code":"86",
            "mobile":"13714643075",
            "gender":null,
            "birthday":null,
            "avatar":null,
            "last_login_time":"2017-08-1816:10:33",
            "user_id":45701,
            "bonus":114, 
            } 
        ```
    - 失败时返回
        ```
            {
                "code":40001,
                "msg":"用户未注册"
            }
        ```

### 六、接口风格
- 使用RESTful架构风格

#### 1 域名
- 应该尽量将API部署在专用域名之下
    ```
    https://api.test.com/
    ```

#### 2 路径
- 路径又称"终点"（endpoint），表示API的具体网址
- 在RESTful架构中，每个网址代表一种资源（resource），所以网址中不能有动词，只能有名词，而且所用的名词往往与数据库的表格名对应。一般来说，数据库中的表都是同种记录的"集合"（collection），所以API中的名词也应该使用复数
    ```
    https://api.test.com/users
    ```

#### 3 HTTP动词
- 对于资源的具体操作类型，由HTTP动词表示
- 常用的HTTP动词有下面四个（括号里是对应的SQL命令）
    - GET(SELECT)：从服务器取出资源（一项或多项）
    - POSE(INSERT)：从服务器新建一个资源
    - PUT(UPDATE)：在服务器更新资源
    - DELETE(DELETE)：在服务器删除资源
-  下面是一些例子
    - GET /v1/rooms：列出房间列表
    - POST /v1/rooms：新建一个房间
    - GET /v1/rooms/{ID}：获取某个指定房间的信息
    - PUT /v1/rooms/{ID}：更新某个指定房间的信息
    - DELETE /v1/rooms/{ID}：删除某个房间 

#### 4 返回结果
- 针对不同操作，服务器向用户返回的结果应该符合以下规范
- 示例如下
    - GET /v1/rooms：列出房间列表（数组）
    - GET /v1/rooms/{ID}：获取某个指定房间的信息（返回单个房间对象）
    - POST /v1/rooms：新建一个房间（返回新生成的房间对象）
    - PUT /v1/rooms/{ID}：更新某个指定房间的信息（返回完整的资源对象）
    - DELETE /v1/rooms/{ID}：删除某个房间（返回一个空文档）

### 七、安全
- 接口安全必须做到以下2点
    - 使用HTTPS协议保证接口数据转输安全
    - 使用Oauth2.0 token机制分隔用户权限
