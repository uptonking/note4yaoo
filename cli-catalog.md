---
title: cli-catalog
tags: [cli]
created: 2019-10-06T10:29:08.772Z
modified: 2021-01-01T22:13:44.013Z
---

# cli-catalog

# browser-devtools

```JS
// 浏览器控制台只输出log不输出行号位置VM信息，方便copy； 将代码中的console.log替换为log
const log = (...args) => queueMicrotask(console.log.bind(console, ...args));
```

# 前端工程化工具相关

```shell
python -m http.server 8000
python2 -m SimpleHTTPServer 8000
```

- prettier

```shell
prettier --config ./.prettierrc.js --write '**/*.{js,jsx,ts,tsx,json}' --ignore-unknown

prettier --loglevel debug --config ./.prettierrc.js --write '**/*.*' --ignore-path=./.prettierignore --ignore-unknown
```

- changelog

```shell
conventional-changelog -p angular -i CHANGELOG.md -s -r 0
```

# git相关
- To get your commit through without running that pre-commit hook, use the `--no-verify` option.
  - git ci和push时都可以用

- git配置
  - cat .git/config
    - 查看本仓库git的配置文件，注意本地和全局配置可能不同；
    - 不论配置命令的大小写，`.gitconfig`中都是小写
  - git config --global init.defaultBranch main 
  - git config --global core.fileMode false 
  - git config --global core.ignoreCase false 
  - git config --global alias.co checkout
  - git config --global alias.br branch
  - git config --global alias.ci commit
  - git config --global alias.st status
  - git config --global core.autocrlf true 
  - git config --global --add --bool push.autoSetupRemote true
    - 本地新分支，自动创建关联，直接push

- "autocrlf" should be "input" on Unix (Mac/Linux) while "true" on Windows. 
  - This is very well-explained on Git's official document under the[ "Formatting and Whitespacing"](https://stackoverflow.com/questions/44720236) section

- git命令别名
  - git config --global alias.lg "log --color --graph --pretty=format:'%C(bold red)%h%C(reset) - %C(bold green)(%cr)%C(bold blue)<%an>%C(reset) -%C(bold yellow)%d%C(reset) %s' --abbrev-commit"
    - %h 表示提交id；
    - %cr 表示提交时间；
    - %an 表示提交人；
    - %d 表示 分支、tag、HEAD 等信息；
    - %s 表示提交的信息。

- debug相关
  - 将远程git仓库里的指定分支拉取到本地（本地不存在的分支）
    - git checkout -b 本地分支名 origin/远程分支名
    - 若提示origin/远程分支名不存在，需要先git fetch --all
  - switch my git repository to a particular commit
    - git checkout -b new_branch 6e559cb
      - With the commit hash (or part of it)
    - git checkout -b new_branch HEAD~4
      - go back 4 commits from HEAD
  - 将某个文件回退到某个commit，常用来处理package.json/lock-file的依赖冲突
    - git checkout c5f567 -- file1/to/restore file2/to/restore

- commit相关
  - 修改最新commit描述信息
    - git commit --amend -m 'new msg'
  - 修改第N条commit描述信息
    - you can use `reword` to be prompted to only change the commit message
    - https://stackoverflow.com/questions/1884474
    - git rebase -i HEAD~n    倒数条第N条，N>=1
  - commit后又修改了，但不想添加记录
    - git add .
    - git commit --amend --no-edit
  - 撤销上次commit的记录，不回滚修改
    - **只撤销本次提交记录，实际修改后的文件仍然存在本地**
    - git reset HEAD~
    - git reset commit_id
  - 撤销 commit, 同时本地删除该 commit 修改：
    - git reset --hard commit_id
    - git reset --hard HEAD~
    - git push origin -f
    - [git放弃修改，放弃增加文件操作](https://blog.csdn.net/ustccw/article/details/79068547)

- clone非master分支、修改克隆下来的文件夹名称
  - `git checkout origin/branchName` 切换分支
  - `git clone -b <branch-name> <repo-url> <destination-folder-name>`

- 删除远程仓库中的文件，如意外提交了node_modules文件夹
  - 另一种方法：直接将远程要删除的文件加入 `.gitignore`

```
git rm --cached 文件/夹名，只删除了缓存，实际文件不会删除
git commit -m '备注'
git push origin 分支
```

- 删除本地和远程两份文件

```
git rm 文件名       // 删除文件
git rm -r 文件夹名   // 删除文件夹 
git add .
git commit -m '备注'
git push origin 分支
```

- 放弃本地修改，用远程覆盖本地

```
git fetch --all
git reset --hard origin/master
git pull
```

- 用本地覆盖远程
  - -f is short for --force

```
git push origin main --force 
```

- Syncing Fork with Parent Repo

```shell
# check if remote exists
git remote -v

# add the remote
git remote add upstream <https... .git>

# fetch the upstream repo
git fetch upstream

# merge the branch
git merge upstream/main

# push the changes
git push

```

- git status命令 
  - Unmerged paths: 下面列出的就是全部冲突文件，挨个解决即可

- git 常用命令
  - `git branch branchName` : 创建新分支
  - `git branch -m master main`: 修改分支名
  - `git checkout branchName startPoint` ：切换到新分支
  - `git checkout -b bName` = `g branch bName` + `g checkout bName`
  - `git merge b` ：将b分支合并到当前分支
    - 执行merge之后，会产生一个新的commit
    - `git merge master feature` ：将master分支合并到feature分支
  - `git rebase` ：功能和 `git merge` 类似，
    - `git checkout feature` + `git rebase master`
    - 将整个feature分支移动到master分支的后面，将master分支上新的提交并过来
    - 不会产生新commit

- 其他命令
  - git stage 作为 git add 的一个同义词
  - git diff --staged 作为 git diff --cached 的相同命令
    - 为了容易理解，推荐大家使用 git stage 和 git diff --staged 这两个命令，
    - 而git add 和 git diff --cached 这两个命令，仅仅为了保持和以前的兼容做保留。
  - git diff 显示当前工作区的文件和stage区文件的差异
  - git diff --staged 显示stage区和HEAD的文件的差异
  - git diff HEAD 显示工作区和上次递交文件的差异
  - 当文件加入了 stage 区以后，如果要从stage删除，则使用 reset, 此时工作区的文件不做任何修改
  - 当文件加入了 stage 区以后，后来又做了一些修改，这时发现后面的修改有问题，想回退到stage的状态，使用 checkout 
  -  git commit -a 并不会作用于第一次新建的文件。 否则容易因此忽略新文件的提交。
  -  git push origin -d release-1.8.27 删除远程分支

- 对于多分支的代码库，将代码从一个分支转移到另一个分支是常见需求。
  - 一种情况是，你需要另一个分支的所有代码变动，那么就采用合并（git merge）
  - 另一种情况是，你只需要部分代码变动（某几个提交），这时可以采用 Cherry pick。
  - git checkout master
  - git cherry-pick commit-id1 commit-id2
    - 将feature分支的commit-id1 id2合并到master

## git-not-yet

- 每次合并远程分支后，会出现干扰性commit
  - merge branch main of github.com:toeverything/toe-editor
# java相关
- maven编译
  - 编译异常后解决了继续上次编译： `mvn <args> -rf :pdi-ce`
  - mvn使用proxy下载依赖： ` mvn clean install -DsocksProxyHost=127.0.0.1 -DsocksProxyPort=1080`
      - 注意验证，saiku下载的jar全是7.8k无效jar
  - 安装本地jar

```

   mvn install:install-file -Dfile=/path/to/local.jar -DgroupId=a.b -DartifactId=name -Dversion=1.0.0 -Dpackaging=jar
  ```

- 切换java版本-基于jenv

```

  jenv add /usr/lib/jvm/adoptopenjdk-8-hotspot-amd64
  使用alias添加同一版本的不同jvm：jenv add dcevm11 /path/to/jdk
  jenv global 11
  注意JAVA_HOME可能未改变，需要手动更新
  export JAVA_HOME=
```

- 切换java版本-基于upadte-alternatives-deprecated

```
  sudo update-alternatives --config java
  sudo update-alternatives --config javac

  /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java  
  /usr/lib/jvm/java-11-openjdk-amd64/bin/java  
  /usr/lib/jvm/java-8-openjdk-amd64/bin/javac   
  /usr/lib/jvm/java-11-openjdk-amd64/bin/javac   
```  
# 视频格式转换

```shell

ffmpeg -i input.flv -codec copy output.mp4
```
