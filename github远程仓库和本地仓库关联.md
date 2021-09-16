### github远程仓库和本地仓库关联



#### 创建远程仓库

- 直接登陆**GitHub**中，新建一个**Repository** ，**十分注意现在新建的仓库默认分支为main**



#### 本地仓库关联远程仓库

##### 自己创建本地仓库

- 找到需要的目录下，右键打开git bash，**本地创建的仓库默认分支还是master**

- 输入以下命令，先本地建立main分支，转到mian分支下

  - **git init**，初始化本地仓库

  - **git checkout -b main**，建立一个新的分支，并转至main分支

  - git checkout main，切换分支到main （可选）

  - git branch，查看当前存在的分支（可选）

  - git merge master ，将master分支合并到main分支上（可选）

  - git pull origin main --allow-unrelated-histories，加上后面这个选项允许不相关历史提交（可选）

  - git branch -D master，删除远程github仓库master分支，同样存在网络原因（可选）

  - **git add .**  ，将本目录下的所有文件添加到本地仓库中

  - **git commit -m “注解”**，添加本次提交的注解信息

  - **git remote add origin https://github.com/xiewende/note.git** ，建立与远程仓库的链接

  - **git push origin main**，将会push到main分支上，此项操作和网络原因有关系，失败后可以多尝试几次

  - git config --global http.sslVerify "false" ，若出现，服务器的SSL证书没有经过第三方机构的签署，这句解决

    

##### 直接克隆建立好的仓库

- 直接克隆刚刚建立好的仓库，**分支就是main分支**
- 输入一下命令，直接clone
  - **git clone https://github.com/xiewende/note.git**  ，克隆仓库到本地链接
  - **git add .**  ，将本目录下的所有文件添加到本地仓库中
  - **git commit -m “注解”**，添加本次提交的注解信息
  - **git push origin main** ，将会push到main分支上，此项操作和网络原因有关系，失败后可以多尝试几次**（注意是main不是master）**
  - 和上面一样，出现SSL证书问题，按照此解决就好



