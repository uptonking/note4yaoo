---
title: cli-catalog
tags: [cli]
created: 2019-10-06T10:29:08.772Z
modified: 2021-01-01T22:13:44.013Z
---

# cli-catalog

# browser-devtools

```JS
// 浏览器控制台只输出log不输出行号位置VM信息，方便copy； 将console.log替换为log
const log = (...args) => queueMicrotask(console.log.bind(console, ...args));
const log = (...args) => queueMicrotask(.bind(console, ...args));
```

# 前端工程化工具相关

```shell
python -m http.server 8000
python2 -m SimpleHTTPServer 8000
```

- prettier

```shell
npx prettier --write '**/*.{js,jsx,ts,tsx,json}'

prettier --config ./.prettierrc.js --write '**/*.{js,jsx,ts,tsx,json}' --ignore-unknown

prettier --loglevel debug --config ./.prettierrc.js --write '**/*.*' --ignore-path=./.prettierignore --ignore-unknown
```

- file

```shell
# remove files
rimraf --glob ./**/*.tsbuildinfo
```

- changelog

```shell
conventional-changelog -p angular -i CHANGELOG.md -s -r 0
```

# typescript

```shell
# show merged compilerOptions
tsc --showconfig
```

# git相关
- To get your commit through without running that pre-commit hook, use the `--no-verify` option.
  - git ci和push时都可以用

- 分支debug相关

```shell
# clone非master分支、修改克隆下来的文件夹名称
git clone -b <branch-name> <repo-url> <destination-folder-name>

# 对于体积很大的仓库，可以在clone时指定只获取最近N次提交
git clone --depth N repo
# 在获取10个提交
git fetch --depth=10
git fetch --unshallow

# 将远程git仓库里的指定分支拉取到本地（本地不存在的分支）
  # 若提示origin/远程分支名不存在，需要先 git fetch --all
git checkout -b 本地分支名 origin/远程分支名
# or
git fetch origin main:main
git fetch origin feature/123
git checkout feature/123

# switch my git repository to a particular commit
# With the commit hash (or part of it)
git checkout -b new_branch 6e559cb
# go back 4 commits from HEAD
git checkout -b new_branch HEAD~4
# 将某个文件回退到某个commit，常用来处理package.json/lock-file的依赖冲突
git checkout c5f567 -- file1/to/restore file2/to/restore

git branch --set-upstream-to=origin/my_branch
git branch -u origin/my_branch

# To rename the current branch
git branch -m newname

# git 列出变更文件 --porcelain 和 --short/-s 相似，但易解析、兼容性更好
git status --porcelain
# Show untracked files
git status -u
```

- commit相关

```shell
# commit后又修改了，但不想添加记录
# if the restart button in jenkin doesn't work, just the git commit --amend --no-edit trick and force push it again
git add .
git commit --amend --no-edit
# 修改最新commit描述信息
git commit --amend -m 'new msg'
# 修改倒数第N条commit描述信息
# you can use `reword` to be prompted to only change the commit message
# https://stackoverflow.com/questions/1884474
git rebase -i HEAD~n    倒数条第N条，N>=1

# trigger CI
git commit --allow-empty -m 'chore: empty commit'

# 撤销上次commit的记录，不回滚修改
# **只撤销本次提交记录，实际修改后的文件仍然存在本地**
git reset HEAD~
git reset commit_id

# 撤销 commit, 同时本地删除该 commit 修改：
# [git放弃修改，放弃增加文件操作，场景较多](https://blog.csdn.net/ustccw/article/details/79068547)
git reset --hard commit_id
git reset --hard HEAD~
git push origin -f

# useful since adding the -f -d flag deletes new directories and files within them as opposed to just -f flag which only deletes new files.
git reset --hard <commitId> && git clean -f -d 

# [Hard reset of a single file](https://stackoverflow.com/questions/7147270/)
git checkout HEAD -- my-file.txt
git checkout upstream/master -- myfile.txt

# 
git checkout -b old-state 0d1d7fc32

# show commits by author 默认大小写敏感
# git log: it is always case sensitive; to make case-insensitive
# git config core.pager "less -IR -" 

# 默认按author排序，但不显示datetime
git shortlog 

git log --author="\(uptonking\)\|\(Jin\)"  --pretty=format:"%h - %an, %ar : %s"
gitk --author="\(uptonking\)\|\(Jin\)"  --pretty=format:"%h - %an, %ar : %s"
# exclude commits by author
gitk --perl-regexp --author='^(?!joe)'
gitk --perl-regexp --author='^(?!jack|jill)'

```

- merge相关

```shell
git rebase --abort
# merge时出现冲突且未处理冲突，如何取消merge
git merge --abort         >= 1.7.4
git reset --merge         >= 1.6.1
git reset --hard
```

- pr相关

```shell
# GitHub cli 最常用的两个命令，当 PR 多了特别救命
gh pr checkout ${num}
gh pr create
```

- [Git commands overview for your future projects](https://twitter.com/davidm_ml/status/1763885692071899264)

- 删除远程仓库中的文件，如意外提交了`node_modules`文件夹
- 一种方法：直接将远程要删除的文件加入 `.gitignore`；
  - 此时vscode显示的文件夹可能没变灰，[gitignore does not ignore folder](https://stackoverflow.com/questions/24410208/)
  - 需要执行 `git rm -r --cached <del-folder>`, 此时本地文件不会删除，但会删除远程文件

```shell
git rm --cached 文件/夹名，只删除了缓存，实际文件不会删除
git commit -m '备注'
git push origin 分支
```

- 删除本地和远程两份文件

```shell
git rm 文件名         // 删除文件
git rm -r 文件夹名    // 删除文件夹 
git add .
git commit -m '备注'
git push origin 分支
```

- 放弃本地修改，用远程覆盖本地

```shell
git fetch --all
git reset --hard origin/master
git pull
```

- 用本地覆盖远程
  - -f is short for --force

```shell
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

git remote rename <old-name> <new-name>
```

- git status命令 
  - Unmerged paths: 下面列出的就是全部冲突文件，挨个解决即可

- git配置相关
  - cat .git/config 查看本仓库git的配置文件，注意本地和全局配置可能不同；
    - 不论配置命令的大小写，`.gitconfig`中都是小写

```shell
git config --global init.defaultBranch main 
git config --global core.fileMode false 
git config --global core.ignoreCase false 
# 让git status输出的包含中文的文件名正确显示
git config --global core.quotepath false

git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status

# 本地新分支，自动创建关联，直接push
git config --global --add --bool push.autoSetupRemote true

# merge时自动检测文件夹重命名
git config --global merge.directoryRenames true
```

- git config --global core.autocrlf true/input
  - `autocrlf` should be "input" on Unix (Mac/Linux) while "true" on Windows. 
  - This is very well-explained on Git's official document under the[ "Formatting and Whitespacing"](https://stackoverflow.com/questions/44720236) section

- git命令别名
  - git config --global alias.lg "log --color --graph --pretty=format:'%C(bold red)%h%C(reset) - %C(bold green)(%cr)%C(bold blue)<%an>%C(reset) -%C(bold yellow)%d%C(reset) %s' --abbrev-commit"
    - %h 表示提交id；
    - %cr 表示提交时间；
    - %an 表示提交人；
    - %d 表示 分支、tag、HEAD 等信息；
    - %s 表示提交的信息。

- git 常用命令

```shell
# 创建新分支
git branch branchName

# 修改分支名
git branch -m master main

# 切换到新分支
git checkout branchName startPoint
# git checkout -b bName = git branch bName  +  git checkout bName

# 将b分支合并到当前分支，执行merge之后，会产生一个新的commit
git merge b
# 将master分支合并到feature分支
git merge master feature

# 使用rebase而不是merge合并
git rebase origin/main

# count commits in a branch
git rev-list --count main/master

# view git history for folder
git log -- path/to/folder
```

- `git rebase` ：功能和 `git merge` 类似，
  - `git checkout feature` + `git rebase master`
  - 将整个feature分支移动到master分支的后面，将master分支上新的提交并过来
  - 不会产生新commit

- git 其他命令
  - `git stage` 作为 git add 的一个同义词
  - git diff --staged 作为 git diff --cached 的相同命令
    - 为了容易理解，推荐大家使用 git stage 和 git diff --staged 这两个命令，
    - 而git add 和 git diff --cached 这两个命令，仅仅为了保持和以前的兼容做保留。
  - git diff 显示当前工作区的文件和stage区文件的差异
  - git diff --staged 显示stage区和HEAD的文件的差异
  - git diff HEAD 显示工作区和上次递交文件的差异
  - 当文件加入了 stage 区以后，如果要从stage删除，则使用 reset, 此时工作区的文件不做任何修改
  - 当文件加入了 stage 区以后，后来又做了一些修改，这时发现后面的修改有问题，想回退到stage的状态，使用 checkout 
  - git commit -a 并不会作用于第一次新建的文件，否则容易因此忽略新文件的提交。
  - git push origin -d release-1.8 删除远程分支

- 对于多分支的代码库，将代码从一个分支转移到另一个分支是常见需求。
  - 一种情况是，你需要另一个分支的所有代码变动，那么就采用合并（git merge）
  - 另一种情况是，你只需要部分代码变动（某几个提交），这时可以采用 Cherry pick。
  - git checkout master
  - git cherry-pick commit-id1 commit-id2
    - 将feature分支的commit-id1 id2合并到master

- git 调试

```sh
GIT_TRACE=2 GIT_CURL_VERBOSE=1 GIT_TRACE_PERFORMANCE=1 git add .  &&  GIT_TRACE=2 GIT_CURL_VERBOSE=1 GIT_TRACE_PERFORMANCE=1 git commit -m 'refactor: remove unused'
```

## git-not-yet

- 每次合并远程分支后，会出现干扰性commit
  - merge branch main of github.com:user/repo
  - 使用git rebase解决

## github-cli

```sh
# List repositories owned by a user or organization.
gh repo list [<owner>] [flags]
gh repo list uptonking --source

# Display the description and the README of a GitHub repository
gh repo view [<repository>] [flags]

# Assigned Issues/PR/CR/Mention
gh status

```

- 自动 sync 所有 fork

```shell
gh repo sync [<destination-repository>] [flags]
# Sync remote repository from another remote repository
gh repo sync owner/repo --source owner2/repo2

# https://twitter.com/tison1096/status/1732739063810334796
gh repo list --fork --visibility public --json owner,name | jq -r 'map(.owner.login + "/" + .name) | .[]' | xargs -t -L1 gh repo sync
```

- [Git by example](https://codapi.org/git/)
# java相关
- maven编译
  - 编译异常后解决了继续上次编译： `mvn <args> -rf :pdi-ce`
  - mvn使用proxy下载依赖： ` mvn clean install -DsocksProxyHost=127.0.0.1 -DsocksProxyPort=1080`
      - 注意验证，saiku下载的jar全是7.8k无效jar
  - 安装本地jar

```shell
mvn install:install-file -Dfile=/path/to/local.jar -DgroupId=a.b -DartifactId=name -Dversion=1.0.0 -Dpackaging=jar
  ```

- 切换java版本-基于jenv

```shell
jenv add /usr/lib/jvm/adoptopenjdk-8-hotspot-amd64
使用alias添加同一版本的不同jvm：jenv add dcevm11 /path/to/jdk
jenv global 11
注意JAVA_HOME可能未改变，需要手动更新
export JAVA_HOME=
```

- 切换java版本-基于upadte-alternatives-deprecated

```shell
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
