# 部署说明

## 前端部署

1. <b> Vue前端构建</b>
    ```
    npm run build  
    ``` 
    构建成功后基本会在配置的dist文件下生成静态文件
2. <b> 静态文件部署 </b>
    将前端构建生成的静态文件复制到后台项目的/dist目录下


## 后台部署

- 操作系统：Ubuntu 18.04LTS

- 部署工具：Gunicorn + Nginx

1. 安装Gunicorn和Nginx
    ```
    pip install gunicorn
    sudo apt install nginx
    ```

2. [运行服务器](https://github.com/SYSU-WebDevelopment-LMTZ/backend/blob/master/readme.md)

3. 修改Nginx配置文件软链接
    ```
    sudo ln -s /home/zhangwx/mycode/system/backend+shangjiaduan+frontend/backend/code/nginx/conf.d/web.conf /etc/nginx/sites-available/default
    ```

4. 进入点餐页面
    ```
    http://localhost/
    ```

- 说明：由于我们没有租云服务器，因此是在局域网内完成项目的部署工作。部署后，系统能正常访问。
