# git基本操作
--- ---

### 1. 基于远端建立分支
```shell
# 基于远端master创建分支new_branch
git checkout -b new_branch origin/master
```

### 2. rebase
多人合作开发时，每个人都会不断的merge到feature分支上，为了规避落后的提交覆盖掉先前的提交，一定要在push前先执行rebase操作。

```
git add -A
git commit -m "备注要有点意义，别瞎写。"
git pull --rebase # 此操作会拉取远端代码，并将上面的commit放到仓库末尾；理解成同步到最新就可以。
git push
```
>注:git pull --rebase可能会引起冲突，比如别人和自己都修改了某段代码，这时需要先解决冲突然后在git push


### 3. 修改远端指向

比如本地分支是基于origin/master拉取的，可以修改到指向为origin/feature1来拉取最新代码

```
git branch -u origin/feature1
git pull --rebase
```

### 4. 开发流程
  * 创建自己的分支
  * 开发后push到自己的分支上
  * Merge Request到feature分支上待测试
  * feature分支Merge Request到master上待发布

### 5. rebase解决冲突
git pull --rebase 冲突 # 比如xx.go文件冲突
```
    a)  在ide里面解决xx.go文件冲突 
    b)  git add xx.go
    c)  git rebase --continue
    不断重复abc三步直到没有冲突
```
### 6. cherry-pick
单独摘取某一个commit到本分支
```
git cherry-pick -x 7ad110fa
git push
```

### 7. 强制覆盖本地代码
```
git fetch --all && git reset --hard origin/master && git pull
```

### 8. 本地分支跟远端分支对应关系
```
git branch -vv
```
