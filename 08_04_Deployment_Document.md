# 部署说明

## 前端部署

1. <b> Vue前端构建</b>
```
npm run build  
```  
构建成功后基本会在配置的dist文件下生成静态html文件

2. <b> 生成的静态代码上传到服务器 </b>  

把生成目录dist里的文件打包上传至服务器(192.168.234.97)
```
scp ./dist.zip root@192.168.234.97:/opt/www/vue-base  
```  
输入服务器登录密码  
上传到服务器静态地址  
```
/opt/www/vue-base 
``` 

3. <b> 解压 dist.zip </b>  
```
unzip dist.zip 
``` 

4. <b> Nginx 配置 </b>   

Nginx安装目录  
```
cd /opt/software/nginx 
```   
进入Nginx安装目录，修改Nginx的配置文件：  
```
vim conf/nginx.conf 
```   
修改如下，root映射到静态代码文件夹：    
```
  location / {    
      #root   html;    
      root   /opt/www/vue-base/dist;    
      index  index.html index.htm;    
  } 
``` 

5. <b> 启动Nignx </b>  

进入Nignx安装目录，执行命令：  
```
./nginx 
```   
重启Nginx  
```
./nginx -s reload
```  

6. <b> 访问 </b>  

http://192.168.234.97


## 后台部署

1. 系统环境：Ubunto 18 /（Windows 10 Virtualenv 配置虚拟环境）

2. MySql安装

3. Python 3.6 + flask 环境配置

4. docker安装

5. [版本配置](requirements.txt)

6. [运行服务器](https://github.com/SYSU-WebDevelopment-LMTZ/backend/blob/master/readme.md)

