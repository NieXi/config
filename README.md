# WiKi
## win10 小狼毫兼容问题(删除注册表):
1. `HKEY_LOCAL_MACHINE/SOFTWARE/Microsoft/CTF/TIP/` 下搜索"小狼毫".
2. 在上一层的 Category 目录下找到所有的 `{13A016DF-560B-46CD-947A-4C3AF1E0E35D}` (一共两个),删除这两个注册表.

## vim-airline 显示问题：
1. 需要特殊字体,从 airline 官网下载.
2. (win)设置 vim 字体:
	- `set guifont=*` 选中想要的字体.
	- 然后再`:set guifont`得到已经临时设置的字体的名称.
	- 在_vimr中添加得到的字体名称.
3. gvim for win 中字体间的空格可以用`_`代替，linux 中可用`\ `代替.

## win10 mysql 的 zip 压缩包安装方式：
1. 账户密码:
        
        username:root
        password:root

2. 解压 zip 压缩包到指定文件夹.
3. 新建一个 my.ini 配置文件：
        
        [mysql]
        ; 设置 mysql 客户端默认字符集
        default-character-set=utf8
        [mysqld]
        ;设置 3306 端口
        port = 3306 
        ; 设置 mysql 的安装目录
        basedir=E:\mysql5.7
        ; 设置 mysql 数据库的数据的存放目录
        datadir=E:\mysql5.7\data
        ; 允许最大连接数
        max_connections=200
        ; 服务端使用的字符集默认为 8 比特编码的 latin1 字符集
        character-set-server=utf8
        ; 创建新表时将使用的默认存储引擎
        default-storage-engine=INNODB 

4. 以管理员身份打开 cmd 窗口后,将目录切换到你的解压文件 bin 目录下.再输入`mysqld install`回车运行就可以了,注意是`mysqld`不是`mysql`.
5. 接下来执行`mysqld  --initialize` 初始化 data 目录.(mysql会自动新建 date 文件夹)
6. 在提示命令管理工具输入如下命令,进入安全模式:`mysqld --defaults-file="E:\mysql5.7\my.ini" --console --skip-grant-tables`,路径根据安装的实际路径修改,保持该窗口运行.
7. 然后以管理员权限打开新的命令提示窗口,cd 到 mysql 的 bin 目录.
8. 修改密码,`use mysql;`,`update user set authentication_string=password("此处输入密码") where user="root"`
9. 刷新数据库`flush privileges;`
10. 添加 mysql 的 bin 目录到 Path 环境变量.
11. [百度经验][1]

## Java 环境变量配置:
- 安装目录结构:
        
        D:\Java\---jdk
                ---jre

- 用户环境变量配置:
        
        JAVA_HOME:      `D:\Java\jdk`(jdk安装目录)
        CLASS_PATH:     `.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;`
        PATH:           `;%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;`

## CapsLock键与L-Ctrl互换:
- 方法一:
    1. `win+R`+`regedit`打开注册表.
    2. `HKEY_LOCAL_MACHINE`-->`System`-->`CurrentControlSet`-->`Control`-->`KeyBoard Layout`(不是Layouts).
    3. 新建二进制值`New`-->`Binary value`.
    4. 重命名:`New Value #1`-->`Scancode Map`.
    5. `Scancode Map`-->`Modify`.
    6. 输入:
            
		    0000  00 00 00 00 00 00 00 00
		    0008  03 00 00 00 1D 00 3A 00
		    0010  3A 00 1D 00 00 00 00 00
		    0018
- 方法二:
    1. 新建一个`caps-to-ctrl.reg`文件:
            
            REGEDIT4
            [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout]
            "Scancode Map"=hex:00 00 00 00 00 00 00 00 03 00 00 00 1D 00 3A 00 3A 00 1D 00 00 00 00 00

    2. 双击导入这个注册表文件,重启,okay.

## PortableGit 设置.ssh:
1. 打开`git-bash.exe`-->`ssh-keygen -t rsa -C “username@example.com”`,然后一路next.
2. 在 user 目录下的 .ssh 文件夹中打开`id_rsa.pub`,把其中的内容填到 github 的 ssh 中.

## 实用的PY:
1. python -m SimpleHTTPServer [port]
2. python -m http.server [port]

## ConEmu
1. Startup-->Command line: `%windir%\system32\bash.exe ~ -cur_console:p1`(直接启动bash,主目录)

[1]:http://jingyan.baidu.com/article/af9f5a2d16fa4d43150a4552.html
