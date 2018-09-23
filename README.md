# 2018秋季学期系统分析与设计课程项目主页

[项目主页](https://sysu-webdevelopment-lmtz.github.io/dashboard/)

### 文档更新流程

- [Git安装](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137396287703354d8c6c01c904c7d9ff056ae23da865a000)

- [添加公钥到Github](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001374385852170d9c7adf13c30429b9660d0eb689dd43a000)

- 如果本地还没有这个文档仓库，需要先把Github仓库克隆到本地
    ```
    git clone git@github.com:SYSU-WebDevelopment-LMTZ/dashboard.git
    ```

- 克隆仓库到本地后，每次修改文档和提交的流程

    - 先pull远程仓库，使得本地仓库与远程仓库同步
        ```
        git pull
        ```

    - 添加/修改markdown文档，必要的时候在index.md添加链接

    - 把本地工作区的修改添加到Git暂存区
        ```
        git add .
        ```

    - 把暂存区的内容提交到本地版本库，-m后面双引号内是本次提交的说明，要按照"<提交说明>_<名字>"的格式写，比如
        ```
        git commit -m "添加团员信息文档_张文晓"
        ```

    - 把本地的修改提交到Github
        ```
        git push origin master
        ```
### 注意事项

1. 不可以直接在Github网页上修改文档/代码，必须在本地修改后调试通过再提交到Github

2. 有时候会出现提交更新到Github后，Github Pages的主页没有更新的情况，这时候可以清除浏览器缓存再等待几分钟。若还是不行，可能是markdown文档修改有误或者提交操作出错