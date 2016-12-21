# 学习git、maven、gitHub、intellij idea
## 一、配置git
#### 1.1 从git官网下载64位的git安装包。[下载git](https://git-scm.com/download/win)
#### 1.2 安装下载的git程序。
###### 1.2.1 点击Next。
![](http://p1.bpimg.com/581766/02c5219bc6c23185.png)
###### 1.2.2 根据自己的需要进行选择，点击Next。
![](http://p1.bpimg.com/581766/5382e2f923664aa9.png)
###### 1.2.3 个人使用选择第二项
![](http://p1.bpimg.com/581766/57319d485933e359.png)
###### 1.2.4 其他步骤默认安装即可。
![](http://p1.bpimg.com/581766/64f19740ea4626e5.png)
![](http://p1.bpimg.com/581766/96efcebc5b3f6d0f.png)
![](http://p1.bpimg.com/581766/c0eb047d6185e633.png)
###### 1.2.5 验证是否安装成功，dos命令中输入git。
![](http://p1.bpimg.com/581766/4ecd5c070db4cb1b.png)
#### 1.3 配置git。
###### 1.3.1 配置账号信息：
`$ git config --global user.name lijie0914`
`$ git config --global user.email 13589214035@163.com`
###### 1.3.2 在终端输入以下命令行：$ ssh-keygen -t rsa -C "13589214035@163.com"
###### 1.3.3 路径选择直接回车使用默认的即可
###### 1.3.4 密码确认不需要，直接回车即可
![](http://i1.piimg.com/581766/cbc372d153a49150.png)
###### 1.3.5 将SSH配置到github中：打开 C:\Users\自己电脑用户名/.ssh，用记事本打开id_rsa.pub，将里边的内容全选复制粘贴到github的SSH keys中。
###### 1.3.6 验证配置是否成功：在命令行输入ssh -T git@github.com
![](http://i1.piimg.com/581766/fb11e0af4db251e8.png)
## 二、配置maven
#### 2.1 安装maven
#### 2.2 在IDEA中配置maven：File-->Settings-->Build,Execution,Deployment-->Build Tools-->Maven
在右侧是Maven home directory选择maven安装的目录即可。
![](http://i1.piimg.com/581766/16d78d7cd0aef24as.png)
## 三、提交项目到GitHub中
#### 3.1 新建一个项目
![](http://i1.piimg.com/581766/1e7e8603e4a258a4.png)
#### 3.2 对项目进行push操作：
###### 3.2.1 首先新建一个库：VCS-->Import into Version Control-->Create Git Repository
![](http://i1.piimg.com/581766/059ff2b480730d27.png)
###### 3.2.2 然后添加文件：VCS-->Git-->Add
![](http://i1.piimg.com/581766/2a423c8a73e35e08.png)
###### 3.2.3 然后进行提交：VCS-->Git-->Commit File
![](http://i1.piimg.com/581766/68b38b2cbde5d5f1.png)
###### 3.2.4 最后Push：VCS---Git---push...(也可以使用快捷键ctrl+shift+k进行push)
![](http://p1.bqimg.com/581766/412b31a6393800e5.png)
#### 3.3 对项目进行pull操作：VCS---Git---pull
![](http://i1.piimg.com/581766/8780c8366a0c3d8a.png)
