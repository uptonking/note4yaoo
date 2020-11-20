---
title: cli-collection
tags: [cli, collection]
created: '2019-10-06T10:29:08.772Z'
modified: '2020-11-14T09:38:09.918Z'
---

# cli-collection

## 前端工程化工具相关

- prettier格式化所有文件

``` 

prettier --write '**/*.*'

prettier --config ./.prettierrc.js --write '**/*.*' --ignore-path=./.prettierignore
```

- changelog

``` 

conventional-changelog -p angular -i CHANGELOG.md -s -r 0
```

## git相关

- clone非master分支
  - `git checkout origin/branchName`
- 删除远程仓库中的文件，如意外提交了node_modules文件夹
  - 另一种方法：直接将远程要删除的文件加入 `.gitignore`

``` 

git rm --cached 文件（夹）名，此时只删除了仓库中的缓存，实际文件不会删除
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
```

- 用本地覆盖远程

``` 

git push origin master --force 
```

- git status命令 
  - Unmerged paths: 下面列出的就是全部冲突文件，挨个解决即可

- git 常用命令
  - `git branch branchName` : 创建新分支
  - `git checkout branchName startPoint` ：切换到新分支
  - `git checkout -b bName` = `g branch bName` + `g checkout bName`
  - `git merge b` ：将b分支合并到当前分支
    - 执行merge之后，会产生一个新的commit
    - `git merge master feature` ：将master分支合并到feature分支
  - `git rebase` ：功能和 `git merge` 类似，
    - `git checkout feature` + `git rebase master`
    - 将整个feature分支移动到master分支的后面，将master分支上新的提交并过来
    - 不会产生新commit

## java相关

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
