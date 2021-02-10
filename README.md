# git_learning


### 一、Git基本设置
```
# 基本的git配置命令

git config --local
git config --global
git config --system

# 设置git配置

git config --list --local
git config --list --global
git config --list --system

# 工作签所需要的最小配置集

git config --global user.name 'liuzheming'
git config --global user.email 'liuzheming@126.com'

```

2. Git创建本地仓库
```
2.1
cd 已经存在的文件夹内
git init

2.2
cd 某个文件夹
git init new_repo  # 会在当前路径下创建new_repo文件夹，并做初始化

```



3. 提交对文件的修改，到本地仓库
```
3.1 
如果不想提交本地所修改的所有代码，可以把本地工作区的指定文件添加到工作空间
git add targetFile

3.2 
如果想要把本地"修改过"的文件，一次性全部都提交到git仓库，可使用-u参数将工作空间的所有文件添加到暂存区
git add -u

3.3
提交代码，commit命令将会把暂存区里的所有代码提交到git仓库
git commit -m 'xxx'

3.4
有一种不推荐的提交方式，即跳过暂存区，直接将本地工作空间的修改作为commit进行提交
git commit -am 'xxx'


```

4. 给文件重命名
```
4.1 原始方法
mv old_name new_name
git delete old_name
git add new_name

git reset --hard # 工作空间、暂存区 中的所有变更都会被清理掉

4.2 简洁方法
git mv old_name new_name

```


5. log命令查看git历史
```
5.1
git log --oneline 简洁的显示当前分支的提交历史
git log -n3 --oneline 查看当前分支的最近3次提交
git log --all --oneline --n4 --graph 显示[所有分支]中最近的4此提交的历史信息，使用图形化界面显示
```

### 二、独自使用Git时的常见场景

6. 分支命令
```
6.1 创建新分支
git checkout -b new_branch_name  创建分支并切换到新分支

6.2 删除分支
git branch -d branch_name_to_delete  删除分支

6.3 强制删除分支
git branch -D branch_name_to_delete  强制删除分支

6.4 切换分支
git checkout branch_name            切换分支

6.5 重命名分支
git branch -m old_branch new_branch 

```

7. 整理commit
```

7.1
修改最近一次commit的message
git commit --amend  # 如果commit已经push到云端,使用--amend修改commit后，需要先pull一次，才能将修改后的内容推送到云端

7.2
修改历史commit的message
git rebase -i xxx  # xxx代表期望修改的commit的前一次commitId
git rebase -i --root # 修改最早的一次commit信息

7.3 合并连续的多个commit变为一个commit
git rebase -i xxx # 打开交互文件后，将期望合并的几次commit前的命令，修改为squash

7.4 合并不连续的多个commit变为一个commit
git rebase -i xxx # 打开交互文件后，先将期望合并的，不连续的commit顺序调整到一起，再需要向前合并的几个commit前的命令，修改为squash



```

8. git diff 命令怎么使用？
```
8.1 修改内容已经提交到暂存区，暂存区文件commit前，需先与历史文件进行对比
git diff --cached 比较暂存区与HEAD所含文件的区别
8.2 修改内容，未提交到暂存区，比较工作区与暂存区的差异
git diff          比较暂存区与工作区的区别

```

9. 撤销 [暂存区、工作区、已提交] 的变更

```
9.1 当前工作区实现了新方案，但是老方案已经提交到了暂存区，怎么办？让暂存区文件恢复成和HEAD一样
git stage                        # 保存工作区的修改
git reset HEAD [-- file_name]    # 将暂存区的修改恢复到HEAD
git diff --cached                # 对比暂存区文件和HEAD，查看是否已经恢复

9.2 工作区的方案不如暂存区，想要把工作区文件恢复到与暂存区一致
git checkout 
git checkout -- index.html

9.3 撤销已经已经提交到本地仓库的commit
git reset --hard [commitId] # 撤销入参所指带commit之后所有提交的变更

```


10. 同步代码

```
git rebase origin master # 将远程的master分支代码同步到当前分支，同步结束后，会被切换至master分支
git merge origin master # 将远程的master分支merge到当前分支，结束后HEAD仍然在当前分支

```


### 三、多人协作使用Git的注意事项

11. commit一旦push到云端，尽量不要再去修改或者整理commit了，反过来说，commit在push之前，应当先整理好
12. push -f 太过危险，是禁止的行为，可以通过设置提交规则，来禁止push -f
