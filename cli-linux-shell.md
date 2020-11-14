---
title: cli-linux-shell
tags: [cli, linux, shell]
created: '2020-11-13T13:07:50.603Z'
modified: '2020-11-13T13:08:39.052Z'
---

# cli-linux-shell

## linux-os

- ### file-tar

- 普通压缩解压缩

``` shell
tar -cvf /tmp/etc.tar  /etc # <==仅打包，不压缩！
tar -czvf /tmp/etc.tar.gz  /etc # <==打包后以gzip压缩,tgz
tar -cjvf /tmp/etc.tar.bz2  /etc # <==打包后以bzip2压缩

tar -xzvf /tmp/etc.tar.gz  /my # 解压到文件夹
```

``` 

-c ：建立一个压缩文件的参数指令(create的意思)；
-x ：解开一个压缩文件的参数指令！
-t ：查看tarfile里面的文件！
  注意，c/x/t仅能存在一个！不可同时存在！因为不能同时压缩与解压。
-z ：是否同时具有 gzip 的属性？亦即是否需要用 gzip 压缩？
-j ：是否同时具有 bzip2 的属性？亦即是否需要用 bzip2 压缩？
-v ：压缩的过程中显示文件！这个常用，但不建议用在背景执行过程！
-f ：使用档名，请留意，在 f 之后要立即接档名喔！不要再加参数！
　　例如使用『 tar -zcvfP tfile sfile』就是错误的写法，
    要写成 『 tar -zcvPf tfile sfile』才对喔！
-p ：使用原文件的原来属性（属性不会依据使用者而变）
-P ：可以使用绝对路径来压缩！
-N ：比后面接的日期(yyyy/mm/dd)还要新的才会被打包进新建的文件！
--exclude FILE：在压缩的过程中，不要将FILE打包！
```

- 分卷压缩
  - `tar -cvzf - filedir | split -d -b 50m - filename`
  - 将./picture文件夹打包，分割为10m的小文件
  - 输出的文件为 filename00、filename01、filename02
  - 如果不加filename，则输出文件为 x00、x01、x02
  - 如果不加参数 -d，则输出aa、ab、ac

``` shell
tar -cvzf - ./picture | split -d -b 10m - picture
```

- 压缩小文件合并
  - `cat picture* > my.tgz`
- 最后解压大压缩包
- ### file-zip
- 分卷压缩时，先压缩成大压缩包，再分卷
  - 分卷文件的名称为a.zip, a.z01, a.z02

``` shell
zip a.zip file
zip -r a.zip folder
zip -s 4m a.zip --out a  # 分割现有zip压缩包

# 直接创建分卷压缩文件
zip -s 100m -r a.zip foo/

```

- 分卷解压时，先合并分卷成大压缩包，再解压

``` shell
zip -F a.zip --out b.zip # b.zip无法通过unzip命令解压，但可通过文件管理器gui解压
# cat a.z* > b.zip # 这样得到的大压缩文件b.zip无法解压
unzip -v b.zip
```

- ### file-cli

- `ln -s fileOrFolder softLinkName`
- 打开目录路径
  - nautilus .
  - xdg-open 直接参数传入要打开的文件，系统会根据文件类型自动调用对应的程序
    - xdg-open a.png/pdf/doc 
    - xdg-open . 会调用nautilus
    - xdg-open https://www.baidu.com 会打开默认浏览器，其中https不可省略

## linux-remote

- ### ssh
- ssh免密登录
  - `ssh-copy-id [-f] [-n] [-i identity file] [-p port] [-o ssh_option] [user@]hostname`
