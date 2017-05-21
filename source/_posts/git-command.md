---
title: git-command
date: 2017-02-21 13:25:29
tags:
    - git
    - git command
categories: others
---
### git常用指令
```
git init                                                  # 初始化本地git仓库（创建新仓库）
git config --global user.name "xxx"                       # 配置用户名
git config --global user.email "xxx@xxx.com"              # 配置邮件
git config --global color.ui true                         # git status等命令自动着色
git config --global color.status auto
git config --global color.diff auto
git config --global color.branch auto
git config --global color.interactive auto
git subtree push --prefix=dist origin gh-pages            # 将dist目录上传到gh-pages分支
git config --global --unset http.proxy                    # remove  proxy configuration on git
git clone git+ssh://git@192.168.53.168/VT.git             # clone远程仓库
git status                                                # 查看当前版本状态（是否修改）
git add xyz                                               # 添加xyz文件至index
git add .                                                 # 增加当前子目录下所有更改过的文件至index
git commit -m 'xxx'                                       # 提交
git commit --amend -m 'xxx'                               # 合并上一次提交（用于反复修改）
git commit -am 'xxx'                                      # 将add和commit合为一步
git rm xxx                                                # 删除index中的文件
git rm -r *                                               # 递归删除
git log                                                   # 显示提交日志
git log -1                                                # 显示1行日志 -n为n行
git log -5
git log --stat                                            # 显示提交日志及相关变动文件
git log -p -m
git show dfb02e6e4f2f7b573337763e5c0013802e392818         # 显示某个提交的详细内容
git show dfb02                                            # 可只用commitid的前几位
git show HEAD                                             # 显示HEAD提交日志
git show HEAD^                                            # 显示HEAD的父（上一个版本）的提交日志 ^^为上两个版本 ^5为上5个版本
git tag                                                   # 显示已存在的tag
git tag -a v2.0 -m 'xxx'                                  # 增加v2.0的tag
git show v2.0                                             # 显示v2.0的日志及详细内容
git log v2.0                                              # 显示v2.0的日志
git diff                                                  # 显示所有未添加至index的变更
git diff --cached                                         # 显示所有已添加index但还未commit的变更
git diff HEAD^                                            # 比较与上一个版本的差异
git diff HEAD -- ./lib                                    # 比较与HEAD版本lib目录的差异
git diff origin/master..master                            # 比较远程分支master上有本地分支master上没有的
git diff origin/master..master --stat                     # 只显示差异的文件，不显示具体内容
git remote add origin git+ssh://git@192.168.53.168/VT.git # 增加远程定义（用于push/pull/fetch）
git branch                                                # 显示本地分支
git branch --contains 50089                               # 显示包含提交50089的分支
git branch -a                                             # 显示所有分支
git branch -r                                             # 显示所有原创分支
git branch --merged                                       # 显示所有已合并到当前分支的分支
git branch --no-merged                                    # 显示所有未合并到当前分支的分支
git branch -m master master_copy                          # 本地分支改名
git checkout -b master_copy                               # 从当前分支创建新分支master_copy并检出
git checkout -b master master_copy                        # 上面的完整版
git checkout features/performance                         # 检出已存在的features/performance分支
git checkout --track hotfixes/BJVEP933                    # 检出远程分支hotfixes/BJVEP933并创建本地跟踪分支
git checkout v2.0                                         # 检出版本v2.0
git checkout -b devel origin/develop                      # 从远程分支develop创建新本地分支devel并检出
git checkout -- README                                    # 检出head版本的README文件（可用于修改错误回退）
git merge origin/master                                   # 合并远程master分支至当前分支
git cherry-pick ff44785404a8e                             # 合并提交ff44785404a8e的修改
git push origin master                                    # 将当前分支push到远程master分支
git push origin :hotfixes/BJVEP933                        # 删除远程仓库的hotfixes/BJVEP933分支
git push --tags                                           # 把所有tag推送到远程仓库
git fetch                                                 # 获取所有远程分支（不更新本地分支，另需merge）
git fetch --prune                                         # 获取所有原创分支并清除服务器上已删掉的分支
git pull origin master                                    # 获取远程分支master并merge到当前分支
git mv README README2                                     # 重命名文件README为README2
git reset --hard HEAD                                     # 将当前版本重置为HEAD（通常用于merge失败回退）
git rebase
git branch -d hotfixes/BJVEP933                           # 删除分支hotfixes/BJVEP933（本分支修改已合并到其他分支）
git branch -D hotfixes/BJVEP933                           # 强制删除分支hotfixes/BJVEP933
git ls-files                                              # 列出git index包含的文件
git show-branch                                           # 图示当前分支历史
git show-branch --all                                     # 图示所有分支历史
git whatchanged                                           # 显示提交历史对应的文件修改
git revert dfb02e6e4f2f7b573337763e5c0013802e392818       # 撤销提交dfb02e6e4f2f7b573337763e5c0013802e392818
git ls-tree HEAD                                          # 内部命令：显示某个git对象
git rev-parse v2.0                                        # 内部命令：显示某个ref对于的SHA1 HASH
git reflog                                                # 显示所有提交，包括孤立节点
git show HEAD@{5}
git show master@{yesterday}                               # 显示master分支昨天的状态
git log --pretty=format:'%h %s' --graph                   # 图示提交日志
git show HEAD~3
git show -s --pretty=raw 2be7fcb476
git stash                                                 # 暂存当前修改，将所有至为HEAD状态
git stash list                                            # 查看所有暂存
git stash show -p stash@{0}                               # 参考第一次暂存
git stash apply stash@{0}                                 # 应用第一次暂存
git grep "delete from"                                    # 文件中搜索文本“delete from”
git grep -e '#define' --and -e SORT_DIRENT
git gc
git fsck
```

### git中 gitignore 文件的正确用法
使用 git 做代码管理工具时，设置 gitignore 是必不可少的流程，一些系统或者 IDE 会在目录下生成与项目不相关的文件，而这些文件我们不期望被提交到仓库之中。理解 gitignore 的 pattern 规则十分重要。

#### PATTERN 规则
关于 Pattern 规则，可以查看 git 的相关[文档](http://git-scm.com/docs/gitignore)：大致有以下几点：
```bash
空行不匹配任何内容，所以可以作为块分隔符；
# 开头表示注释，如果相匹配 #，可以在前面加一个反斜杠，即 \#；
除非加了反斜杠，否则一连串的空格会被忽略；
如果在匹配的内容前面加上 !，则这些匹配过的部分将被移出，如果要匹配以 ! 开头的内容，需要加上反斜杠，如 \!important.txt；
如果一个匹配 pattern 后面有一个斜杠，如 foo/，则默认会匹配所有（包含父子文件夹）中的 foo 文件夹内容，并且它不会匹配单个的文件；
如果一个匹配 pattern 不包含斜杠，如 foo，Git 会将其作为一个 shell 的查找命令匹配内容。
```
需要注意的 **：
- 如果一个 pattern 以 ** 开头，如 **/foo，最后会匹配所有文件夹下的 foo 文件(夹)；
- 如果一个 pattern 以 /** 开头，如 abc/**，则表示匹配 abc 目录下的所有内容（(relative to the location of the .gitignore file, with infinite depth)；
- 如果一个 pattern 中间包含 **，如 a/**/b，则会匹配 a/b、a/x/b、a/x/y/b以及所有类似的内容。

#### gitignore 相关的问题
匹配示例
如果我们要匹配 ‘foo’ 目录下除去 ‘foo/bar/‘ 的内容，可以这样做：
```bash
foo/
!foo/bar/
```
如果要匹配所有目录下的 node_modules 文件夹，只需要这样做：
```bash
node_modules/
```
如果要匹配所有的 json 文件，可以这样做：
```bash
*.json
```
git 操作中，add 之后再加入 gitignore
Git 操作中经常会出现这样的问题，当我们 git add 之后，突然想起来要添加一个 gitignore 文件，但是一些诸如 node_modules/, cache/ 等文件已经被 add 进去了，这些文件不会被 ignore 掉，怎么办？
最直接的方式是：
```bash
# 这一步的操作相当于回到 git add 上一步
git rm -r --cached .
# 然后重新 add
git add  .
git commit -m "fixed untracked files"
```
git 添加空文件夹
Git 默认是不添加空文件夹的，如果一定要加入这个文件夹，有以下方案：
```bash
在文件夹添加文件，然后删除
在文件夹中添加一个 .gitkeep 文件
```
让 git 不要添加 gitignore 文件,可以 add 后再 remove 掉：
```bash
git rm -r --cached .gitignore
```
Git 操作涉及的命令巨多，但是日常开发中用到的就那么几个，把原理搞清楚，用起来得心应手。