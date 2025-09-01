## Git常用指令

### 提交

只要是文件有变化，想提交到本地仓库中，那就先执行git add，再执行git commit。

<img src="C:\Users\10251\AppData\Roaming\Typora\typora-user-images\image-20250406152735680.png" alt="image-20250406152735680" style="zoom:50%;" />

查看所有文件的状态：git status

添加到暂存区：git add ./文件名  (工作区->暂存区)

从暂存区提交到本地仓库：git commit -m "注释"   (暂存区->本地仓库)

查看本地仓库的历史提交记录：git log或者git log [options]

<img src="C:\Users\10251\AppData\Roaming\Typora\typora-user-images\image-20250406155205532.png" alt="image-20250406155205532" style="zoom:50%;" />

版本回退：git reset --hard commitID。其中commitID可以使用git log或git-log指令查看

查看已经删除的提交记录：git reflog

### 分支

(master)就是分支的体现，HEAD指向谁谁就是当前分支。

查看有哪些分支：git branch

新创建一个分支：git branch 分支名字

切换分支：git checkout 分支名字

直接切换到一个不存在的分支(创建并切换)：git checkout -b 分支名

将一个分支dev01上的修改全部**合并**到另一个分支master上：先转到master分支上，再用git merge dev01

删除分支，不能删除当前分支，只能删除其他分支：

​	git branch -d 分支名，删除分支时会进行各种检查。

​	git branch -D 分支名，不进行任何检查，强制删除。

### 解决冲突

当两个分支上对文件的修改可能会存在冲突，例如同时修改了同一个文件的同一行，这时就需要手动解决冲突，解决冲突步骤如下:
	1.处理文件中冲突的地方。
	2.将解决完冲突的文件加入暂存区(add)。
	3.提交到仓库(commit)。

<img src="C:\Users\10251\AppData\Roaming\Typora\typora-user-images\image-20250409102317202.png" alt="image-20250409102317202" style="zoom:50%;" />



## Git远程仓库

### 工作流程图

<img src="C:\Users\10251\AppData\Roaming\Typora\typora-user-images\image-20250409102517668.png" alt="image-20250409102517668" style="zoom:50%;" />

创建仓库：

<img src="C:\Users\10251\AppData\Roaming\Typora\typora-user-images\image-20250409103029283.png" alt="image-20250409103029283" style="zoom:50%;" />

之后配置SSH公钥：

​	生成SSH公钥。

​		ssh-keygen -t rsa

​		不断回车

​			如果公钥已经存在，则自动覆盖。

​	Gitee设置账户公钥

​		获取公钥

​			cat ~/.ssh/id_rsa.pub

<img src="C:\Users\10251\AppData\Roaming\Typora\typora-user-images\image-20250409103545603.png" alt="image-20250409103545603" style="zoom:50%;" />

​	验证是否配置成功

​		ssh -T git@gitee.com

再进行远程连接：

<img src="C:\Users\10251\AppData\Roaming\Typora\typora-user-images\image-20250409104803370.png" alt="image-20250409104803370" style="zoom:50%;" />

添加远程仓库

![image-20250409104949216](C:\Users\10251\AppData\Roaming\Typora\typora-user-images\image-20250409104949216.png)

查看远程仓库

![image-20250409105004904](C:\Users\10251\AppData\Roaming\Typora\typora-user-images\image-20250409105004904.png)

推送到远程仓库

<img src="C:\Users\10251\AppData\Roaming\Typora\typora-user-images\image-20250409105046298.png" alt="image-20250409105046298" style="zoom:67%;" />

删除命名的远程仓库origin

![image-20250409105710002](C:\Users\10251\AppData\Roaming\Typora\typora-user-images\image-20250409105710002.png)







# 简单上传全流程：

1、先创建一个仓库，设置好repository name(就是项目名称)，description可选想设就设，接着设置公开还是私有，勾选Add a REDME file。点击创建仓库，会生成一个链接。

2、安装git，使用git config -l来查看配置情况。

3、使用git config --global user.name "github的用户名"

4、使用git config --global user.email "github绑定的邮箱" ，使用git config -l来查看是否配置成功。

5、使用ssh-keygen -t rsa创建公钥，不断回车，如果公钥已经存在，则自动覆盖。生成的公钥存放在"C:\Users\admin\.ssh\id_rsa.pub"路径下，打开这个id_rsa.pub文件，全选复制，然后到github中找到设置中的SSH and GPG keys，填一个title，然后将公钥粘贴到Key框中保存。

6、在git中使用ssh -T git@github.com测试是否连接成功。

7、在桌面上创建一个临时文件夹，在临时文件夹中右键点击git Bash Here使用git clone 仓库链接。先把github上创建的新仓库克隆下来(因为会有个隐藏的.git文件)， 把想上传的项目文件复制到克隆下来的文件夹中，那就在那个文件夹下右键点击git Bash Here。

8、先使用git status查看未上传的文件。

9、使用git add .将新加入进来的文件暂存到暂存区，再使用git commit -m "本次提交的描述信息"提交到本地仓库。

10、使用git push上传到github上。此时可能会出现连接断开的提示，多进行git push就可以了