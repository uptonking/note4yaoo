---
title: cli-scripts-linux-shell
tags: [cli, linux, scripts, shell]
created: 2020-11-13T13:07:50.603Z
modified: 2023-01-07T15:58:14.300Z
---

# cli-scripts-linux-shell

# guide

# ubuntu
- shell工具

```shell

# 查看端口占用
sudo netstat -tunlp|grep 8000
sudo lsof -i:8000
 
# 运行程序后关闭命令行终端 https://askubuntu.com/questions/429969
# "&> /dev/null &" redirects the output of nohup such that you do not have logs
# 通过自定义系统菜单可回避此问题
nohup firefox &> /dev/null &
# https://stackoverflow.com/questions/72538095/nohup-with-nested-quotes-and-subshell
nohup bash -c 'echo "some text $(aws ... | tail -1)" >> myFile.txt' &

# base64解码
echo aHR0cHM6Ly9tYXMudG8vQG9jYXZ1ZQo= | base64 -d

```

- 系统配置相关

```shell
# intall a version
sudo apt-get install -y apache2=2.3.35-4ubuntu1

# 会删除软件包而保留软件的配置文件
apt remove
# 会同时清除软件包和软件的配置文件
apt purge

# 刷新dns缓存
resolvectl flush-caches
# check the dns cache size 
resolvectl statistics
```

# file

```shell

cp -r source_folder /path/to/destination_folder/

```

## file-cli

- `ln -s fileOrFolder softLinkName`

- 查看文件大小
  - `ls -lh`/ `ll -h` 会显示当前目录下的所有直接文件和直接文件夹的大小
    - 大小基于1024
  - du -h 会显示当前目录的大小，以及当前目录所有子目录的大小；但不会显示当前目录下文件的大小和数量
  - du -ah 会显示当前目录的大小，以及所有子孙目录和文件的大小，被打平了
    - 大小基于1024

- 打开目录路径
  - nautilus .
  - xdg-open 通过参数传入要打开的文件，系统会根据文件类型自动调用对应的程序
    - xdg-open a.png/pdf/doc 
    - xdg-open . 会调用nautilus
    - xdg-open https://www.baidu.com 会打开默认浏览器，其中https不可省略

## tar

### 普通压缩解压缩

```shell
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

### 分卷压缩

- `tar -cvzf - filedir | split -d -b 50m - filename`
- 将./picture文件夹打包，分割为10m的小文件
- 输出的文件为 filename00、filename01、filename02
- 如果不加filename，则输出文件为 x00、x01、x02
- 如果不加参数 -d，则输出aa、ab、ac

```shell
tar -cvzf - ./picture | split -d -b 10m - picture
```

### 压缩小文件合并

- `cat picture* > my.tgz`

- 最后解压大的压缩包

## file-zip

- 分卷压缩时，先压缩成大压缩包，再分卷
  - 分卷文件的名称为a.zip, a.z01, a.z02

```shell
zip a.zip file
zip -r a.zip folder
zip -s 4m a.zip --out a  # 分割现有zip压缩包

# 直接创建分卷压缩文件
zip -s 100m -r a.zip foo/

```

- 分卷解压时，先合并分卷成大压缩包，再解压

```shell
zip -F a.zip --out b.zip # b.zip无法通过unzip命令解压，但可通过文件管理器gui解压
# cat a.z* > b.zip # 这样得到的大压缩文件b.zip无法解压
unzip -v b.zip
```

# account
- [Change all files and folders permissions of a directory to 644/755](https://stackoverflow.com/questions/18817744)
- 修改所有子目录和子目录下的文件的权限为755/644
  - `sudo chmod -R a=r, u+w, a+X ./garden/`
  - 注意逗号间无空格
- 实测ubuntu的yaoo用户的home目录及文件权限分别为775和664
  - [My ubuntu default permissions suddenly changed from 644 to 664?](https://askubuntu.com/questions/1321256)
    - This depends on the default umask which is different for normal users and the root user.
    - normal user:  0002,  775/664
    - root user:    0022,  755/644
- 查看当前目录所有文件夹和文件的权限 
  - find . -maxdepth 1 -printf "%m  %f\n" 

- ssh相关权限
  - sudo chmod 700 ~/.ssh
  - sudo chmod 600 ~/.ssh/id_rsa
  - sudo chmod 600 ~/.ssh/id_rsa.pub

- sudo vs su
  - `su account`
    - 切换到某某用户模式，提示输入密码时该密码为切换后账户的密码，用法为“su 账户名称”。
    - 如果后面不加账户时系统默认为root账户，密码也为超级账户的密码。
    - 没有时间限制。
    - su root的权限太大，所以诞生了sudo
  - `sudo`
    - 暂时切换到超级用户模式以执行超级用户权限，提示输入密码时该密码为当前用户的密码，而不是超级账户的密码。
    - 不过有时间限制，Ubuntu默认为一次时长15分钟。
    - 并不是所有的用户都可以执行sudo命令, 只有在sudoers文件中存在的用户才能执行
    - 使用 `sudo -u username` 会指定特定用户的身份执行
  - `sudo -i`
    - 为了频繁的执行某些只有超级用户才能执行的权限，而不用每次输入密码，可以使用该命令。提示输入密码时该密码为当前账户的密码。
    - 没有时间限制。执行该命令后提示符变为“#”而不是“$”。
    - 想退回普通账户时可以执行“exit”或“logout” 。
  - `sudo s`
    - 环境用的是当前用户本身的环境（只切换shell环境）

- `su` vs `su -`
  - su 和 su - 进入的目录是不一样的
    - su切换成root用户以后，pwd一下，发现工作目录仍然是普通用户的工作目录；
    - 而用`su -`命令切换以后，工作目录变成root的工作目录了。
  - su会保持前者的用户环境, 而 `su -` 会新建一个目的用户的环境
    - `su`只是切换了root身份，但shell环境仍然是普通用户的shell；
    - `su -`连用户身份和Shell环境一起切换成root身份了。
    - 只有切换了Shell环境才不会出现PATH环境变量报command not found的错误
    - 用`echo $PATH`命令看一下su和su - 后的环境变量已经变了。
  - su 会保持当前用户的环境, 在某些情况下使用当前用户比管理员能更好的解决问题
    - 比如重现或者debug问题时,在当前用户环境下更高效
  - 当然 su 在很多情况下是不建议使用的, 或者说是相当危险的. 
    - 因为这会给非root用户更改系统文件或数据的权限
# os
- 系统变量或环境
  - env: 打印所有环境变量
  - locale: 打印各种LANG, LC_TIME

- 查看所有用户
  - cat /etc/passwd
    - 看第三个参数:500以上的,就是后面建的用户了，其它则为系统的用户
    - /etc/shadow和/etc/passwd系统存在的所有用户名
    - /etc/group文件包含所有组
- 创建新用户
  - 使用`useradd`时，如果后面不添加任何参数选项如`sudo useradd test`，创建出来的用户将是默认“三无”用户：一无Home Directory，二无密码，三无系统Shell。
  - 使用`adduser`时，创建用户的过程更像是一种人机对话，系统会提示你输入各种信息，然后会根据这些信息帮你创建新用户。
    - adduser会提示设置密码，而useradd不会。
  - adduser更适合初级使用者，因为不用去记那些繁琐的参数选项，要跟着系统的提示
  - useradd比较适合有些高阶经验的使用者，往往一行命令加参数就能解决很多问题
- 给已创建的用户testuser设置密码
  - passwd testuser
- 删除用户testuser
  - userdel testuser
- 用户组
  - groupadd testgroup    组的添加
  - groupdel testgroup    组的删除
# linux-remote

## ssh

- ssh免密登录
  - `ssh-copy-id [-f] [-n] [-i identity file] [-p port] [-o ssh_option] [user@]hostname`
# linux-hardware
- sudo lshw

```

yaoohpu18                   
    description: Notebook
    product: HP ENVY Notebook (Y8H74PA#AB2)
    vendor: HP
    version: Type1ProductConfigId
    serial: 5CG6404VT0
    width: 64 bits
    configuration: administrator_password=disabled boot=normal chassis=notebook ...
  *-core
    description: Motherboard
    product: 81D1
    vendor: HP
    physical id: 0
    version: KBC Version 87.13
    serial: PFXGH00WB453FZ
    slot: Type2 - Board Chassis Location
  *-firmware
      description: BIOS
      vendor: Insyde
      physical id: 0
      version: F.21
      date: 07/08/2016
      size: 128KiB
      capacity: 6MiB
  *-cpu
    description: CPU
    product: Intel(R) Core(TM) i7-7500U CPU @ 2.70GHz
    vendor: Intel Corp.
    physical id: 4
    bus info: cpu@0
    version: Intel(R) Core(TM) i7-7500U CPU @ 2.70GHz
    serial: To Be Filled By O.E.M.
    slot: U3E1
    size: 3345MHz
    capacity: 4005MHz
    width: 64 bits
    clock: 100MHz
  *-memory
    description: System Memory
    physical id: 26
    slot: System board or motherboard
    size: 32GiB
    *-bank:0
        description: SODIMM DDR4 Synchronous 2133 MHz (0.5 ns)
        product: KHX2133C13S4/16G
        vendor: Kingston
        physical id: 0
        serial: 6C3B6634
        slot: Bottom-Slot 1(left)
        size: 16GiB
        width: 64 bits
        clock: 2133MHz (0.5ns)
  *-storage
    description: Non-Volatile memory controller
    product: NVMe SSD Controller SM951/PM951
    vendor: Samsung Electronics Co Ltd
    physical id: 0
    bus info: pci@0000:03:00.0
    version: 01
    width: 64 bits
    clock: 33MHz
    capabilities: storage pm msi pciexpress msix nvm_express bus_master cap_list
    configuration: driver=nvme latency=0
  *-sata
    description: SATA controller
    product: Sunrise Point-LP SATA Controller [AHCI mode]
    vendor: Intel Corporation
    physical id: 17
    bus info: pci@0000:00:17.0
    version: 21
    width: 32 bits
    clock: 66MHz
    capabilities: sata msi pm ahci_1.0 bus_master cap_list
    configuration: driver=ahci latency=0
```

- lscpu
- lsblk
# discuss
- ## 

- ## 

- ## 

- ## If I have no idea what's occupying a specific port, I run this command. It gives me a PID so I can kill the process.
- https://twitter.com/alex35mil/status/1725091399337480413
  - https://github.com/alex35mil/dotfiles/blob/47f4cfb5f4c165f5d84e2e42cb57db61e4bd32da/home/.config/shell/shortcuts.sh#L146-L170
