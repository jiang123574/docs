常用操作：
```sh
git config --global user.name "lillusory" #//全局用户
git config --global user.email "xueduanli@163.com"  #全局邮箱
git init #初始化
git add . #或某个文件，某些文件
git commit -m 'fix ' #提交信息
git status #查看当前版本库状态
git diff 文件 1 文件 2   #对文件进行比较（也可在版本之间进行比较，后面文件均替换为版本号） 
git push #推送
git pull #拉取
git merge #合并指定分支到当前分支
git checkout +文件  #，表示  撤销对某文件的修改; + 分支，表示切换分支
git rm #文件  删除某文件
git clone #克隆
git checkout -b +分支，表示创建新分支（非 master 分支）
git branch 查看当前分支； + -a 表示查看所有分支 
git branch -d +分支 删除某分支

```

远程仓库

```
git remote add origin + 远程 git 地址 (例如 git@github.com:1900/reviewgit.git)
```

ssh
```sh
ssh-keygen -t rsa -C "你的邮箱地址" #生成sshkey
cat ~/.ssh/id_rsa.pub #查看公钥

```