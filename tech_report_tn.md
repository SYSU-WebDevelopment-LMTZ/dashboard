## axios在vue-cli项目中的封装使用
#### by 18214663

### <b>axios介绍</b>  
axios是一个promise实现的http库，符合最新的ES规范。我们为啥要用这个东西呢，主要有以下几个原因：
- 从浏览器中创建 XMLHttpRequests
- 从 node.js 创建 http 请求
- 拦截请求和响应
- 转换请求数据和响应数据
- 支持 Promise API（可以配合ES7的async await使用，解决回调地狱）
- 客户端支持防止CSRF
- 提供了一些并发请求的接口
- 轻量，体积小

### <b>使用 cnpm 安装 axios</b>
```
cnpm install axios --save
```  
安装其他插件的时候，可以直接在 main.js 中引入并 Vue.use()，但是 axios 并不能 use，只能每个需要发送请求的组件中即时引入
为了解决这个问题，有两种开发思路，一是在引入 axios 之后，修改原型链，二是结合 Vuex，封装一个 aciton。这里只说修改原型链的方式

### <b>首先在 main.js 中引入 axios</b>
```
import axios from 'axios'
```
这时候如果在其它的组件中，是无法使用 axios 命令的。所以我们将 axios 改写为 Vue 的原型属性
```
Vue.prototype.$http= axios
```
在 main.js 中添加了这两行代码之后，就能直接在组件的 methods 中使用 $http命令，例如
```
methods: {
    show() {
      this.$http({
        method: 'get',
        url: '/user',
        data: {
          name: 'virus'
        }
     })
  }
```

### <b>配置 axios</b>
实际上只有 url 是必须的，完整的 api 可以参考https://www.kancloud.cn/yunye/axios/234845

- 对于get请求
```
    axios.get('/user', {
          params:{
                name:"virus"  
          }
    })
```
- 对于post请求
```
  axios.post('/user',{
      name:"virus" 
  })
```
- 一次性并发多个请求
```
function getUserAccount(){
  return axios.get('/user/12345');
}
function getUserPermissions(){
  return axios.get('/user/12345/permissions');
}
axios.all([getUserAccount(),getUserPermissions()])
  .then(axios.spread(function(acct,perms){
    //当这两个请求都完成的时候会触发这个函数，两个参数分别代表返回的结果
  }))
```
- axios可以通过配置（config）来发送请求
```
//发送一个`POST`请求
axios({
    method:"POST",
    url:'/user/1111',
    data:{
      name:"virus" 
    }
});
```
完整的请求还应当包括 .then 和 .catch  
```
   .then(function(res){
          console.log(res)
        })
    .catch(function(err){
          console.log(err)
        })
```
当请求成功时，会执行 .then，否则执行 .catch  
这两个回调函数都有各自独立的作用域，如果直接在里面访问 this，无法访问到 Vue 实例,这时只要添加一个 .bind(this) 就能解决这个问题。(如果使用的是es6箭头函数就不存在这样的问题)
```
    .then(function(res){
          console.log(this.data)
     }.bind(this))
```
### <b>vue开发请求本地模拟数据的配置方法</b>
在做开发的时候我们可能会遇到本地模拟数据的情况，这时候我们就要模拟本地数据了
```
//对于新版本的webpack
//修改webpack.dev.conf.js
//首先
const express = require('express')
const app = express()
var data = require('../data.json')//加载本地数据文件
var apiRoutes = express.Router()
app.use('/api', apiRoutes）

//然后在devServer配置选项里面添加下面的代码
before(app){
  app.get("/api/seller",(req,res)=>{
    res.json({
      data:data.seller
    })
  })
}
```
### <b>补充</b>
vue cli脚手架前端调后端数据接口时候的本地代理跨域问题，如我在本地localhost访问接口  
 http://425.00.100.100:888/  
是要跨域的，浏览器的安全策略，会报错，在webpack配置一下proxyTable就OK了，如下 config/index.js
```
dev: {
    加入以下
    proxyTable: {
      '/api': {
        target: 'http://425.0.100.100:8888/',//设置你调用的接口域名和端口号 别忘了加http
        changeOrigin: true,//如果需要跨域
        pathRewrite: {
          '^/api': '/'
                //这里理解成用面的地址，
                后面组件中我们掉接口时直接用api代替 比如我要调
                用'http://425.0.100.100:8888/user/add'，直接写‘/api/user/add’即可
        }
      }
    },
```






