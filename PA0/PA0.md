> Debian 参考手册：[https://www.debian.org/doc/manuals/debian-reference/](https://www.debian.org/doc/manuals/debian-reference/)
>
> C/C++ 资源：[https://www.cprogramming.com/](https://www.cprogramming.com/)

# 实验记录

1. 本实验说明中建议使用 Debian, Docker 针对 Debian 有指定的安装教程 [链接在此](https://docs.docker.com/install/linux/docker-ce/debian/)

    >安装时可以使用 `lsb_release -a` 命令来查看 Linux 版本

2. Docker 的简单介绍

    Docker image =》 container？概念？？？？？？

3. PA0-First Exploration with GNU/Linux 中提到的 `detach mode 分离模式` 大概就是输入命令之后只返回了 container 的标签，要通过 SSH 登录到 container

    > SSH 的端口之类的设置在命令 `docker create ...` 中指定

4. Package Management 包管理？？？？？？？？？

5. **PA0-Installing Tools-Installing tools for PAs 中执行 `apt-get install gcc-doc` 出错，提示  `E:Package 'gcc-doc' has no installation candidate` ，是因为软件包分类问题，Debian 的软件包分类有 main, contrib, non-free，其中前两个符合 DFSG，会自动添加，具体区别见 [链接](https://blog.csdn.net/gong_xucheng/article/details/53886271)**

    解决：修改或添加 /etc/apt/sources.list 文件中的记录，详见 [链接](https://unix.stackexchange.com/questions/287075/why-cant-i-fetch-the-gcc-doc-package-on-debian)

    > 在 [这里](https://www.debian.org/distrib/packages) 可以搜索到 gcc-doc 的包不在 stable 中，在 jessie, stretch, buster-backports, bullseye, sid 中存在，所以在 sources.list 中添加其中一个就行

6. Vim

    1. 可以使用命令 `vimtutor` 进行 vim 的入门练习

        > `dd` 删除行之后还会在后台保存删除的行，可以使用 `p` 来粘贴该行
        >
        > `ce` 可以删除该单词光标及以后的字母，再进入 Insert mode（可以用来修改多个连续字母错误的单词）**[其中，`c` 为 change 的意思，还可以为 `c$` 修改到行尾]**
        >
        > `CTRL+g` 可以显示当前文件和状态
        >
        > 使用 `/` 或 `?` 搜索之后可以使用 `CTRL+o` 回到原来的位置，`CTRL+I` 往前跳跃
        >
        > `%` 可以用来寻找配对的括号
        >
        > `:#,#s/old/new/g` #为行数，可以在指定行数内修改所有的匹配项；`:%s/old/new/g` 修改整个文件的匹配项； `:%s/old/new/gc` 选中整个文件的匹配项但逐个提示是否需要修改 **[其中，`s` 为 substitute 替换 的意思]**
        >
        > `:!ls` 看起来没有反应是因为当前文件夹为空 **[其中，命令前的 `!` 才是说明 shell 命名而不是 vim 的命令]**
        >
        > `v` 为可视化选择
        >
        > `:r filename` 可以在光标处添加 filename 文件的内容
        >
        > `O` (uppercase) 在光标上方创建新行，lowercase 在光标下方创建新行
        >
        > `#e` 跳到第#个单词的最后一个字母上，#默认为1
        >
        > `R` 可以达到类似 `ce` 的效果但事先不删除单词
        >
        > `y` 为 yank复制 的意思，`p` 为 paste粘贴 的意思

    2. vimrc 配置文件的部分解释

        ```
        setlocal noswapfile " 不要生成swap文件
        set bufhidden=hide " 当buffer被丢弃的时候隐藏它
        colorscheme evening " 设定配色方案
        set number " 显示行号
        set cursorline " 突出显示当前行
        set ruler " 打开状态栏标尺
        set shiftwidth=4 " 设定 << 和 >> 命令移动时的宽度为 4
        set softtabstop=4 " 使得按退格键时可以一次删掉 4 个空格
        set tabstop=4 " 设定 tab 长度为 4
        set nobackup " 覆盖文件时不备份
        set autochdir " 自动切换当前目录为当前文件所在的目录
        set backupcopy=yes " 设置备份时的行为为覆盖
        set hlsearch " 搜索时高亮显示被找到的文本
        set noerrorbells " 关闭错误信息响铃
        set novisualbell " 关闭使用可视响铃代替呼叫
        set t_vb= " 置空错误铃声的终端代码
        set matchtime=2 " 短暂跳转到匹配括号的时间
        set magic " 设置魔术
        set smartindent " 开启新行时使用智能自动缩进
        set backspace=indent,eol,start " 不设定在插入状态无法用退格键和 Delete 键删除回车符
        set cmdheight=1 " 设定命令行的行数为 1
        set laststatus=2 " 显示状态栏 (默认值为 1, 无法显示状态栏)
        set statusline=\ %<%F[%1*%M%*%n%R%H]%=\ %y\ %0(%{&fileformat}\ %{&encoding}\ Ln\ %l,\ Col\ %c/%L%) " 设置在状态行显示的信息
        set foldenable " 开始折叠
        set foldmethod=syntax " 设置语法折叠
        set foldcolumn=0 " 设置折叠区域的宽度
        setlocal foldlevel=1 " 设置折叠层数为 1
        nnoremap <space> @=((foldclosed(line('.')) < 0) ? 'zc' : 'zo')<CR> " 用空格键来开关折叠
        ```

7. Man

    ```
    Manual page 主要包含的小节
    - NAME - 命令名
    - SYNOPSIS - 使用方法大纲
    - CONFIGURATION - 配置
    - DESCRIPTION - 功能说明
    - OPTIONS - 可选参数说明
    - EXIT STATUS - 退出状态, 这是一个返回给父进程的值
    - RETURN VALUE - 返回值
    - ERRORS - 可能出现的错误类型
    - ENVIRONMENT - 环境变量
    - FILES - 相关配置文件
    - VERSIONS - 版本
    - CONFORMING TO - 符合的规范
    - NOTES - 使用注意事项
    - BUGS - 已经发现的bug
    - EXAMPLE - 一些例子
    - AUTHORS - 作者
    - SEE ALSO - 功能或操作对象相近的其它命令
    ```

8. gcc 编译后的可执行文件的默认名字 a.out 代表 assembler output

9. GDB

   ```
   1. $gdb <可执行文件>
   2. 常用命令
   	设置断点：(gdb)break <源文件的代码行数>
   	运行：(gdb)run
   	逐行运行：
   		(gdb)next（不跳转到函数里面）
   		(gdb)step（会跳转到函数里面）
   	程序停止时查看相邻10行代码：(gdb)list
   	打印参数：(gdb)print <变量>
   	修改参数：(gdb)set <变量> = <变量值>
   	设置观察点(Watchpoints)：(gdb)watch <变量>
   	继续执行：(gdb)continue
   	重复上一个命令：(gdb)<回车键>
   3. (gdb)quit
   ```

10. Tmux

  ```
  1. 基本概念
  	session 会话：一个服务器可以包含多个会话
  	window 窗口：一个会话可以包含多个窗口
  	pane 面板：一个窗口可以包含多个面板
  2. 面板的基本使用（注意逗号后面的要加 shift）
  	新建会话：$ tmux
  	关闭会话：$ CTRL+b,&
  	删除面板：$ CTRL+b,X
  	水平分屏：$ CTRL+b,"
  	垂直分屏：$ CTRL+b,%
  	暂时切换回Shell：$ CTRL+b,d
  		返回tmux：$ tmux attach-session -t 0
      分屏间移动：$ CTRL+b,方向键
  ```

11. Docker

    ```
    1. 基本使用：（注意，都是在主机中输入的命令）
    	docker start <container_name> # ics-vm
    	ssh -p 20022 username@127.0.0.1
    	
    	docker stop <container_name> # ics-vm
    2. 要从容器中退出直接使用 exit
    3. 容器和主机之间传输文件（注意，都是在主机中输入的命令）
    	scp -P 20022 username@127.0.0.1:SRC_PATH HOST_PATH # 把文件从容器复制到主机，-P 指使用指定端口号
    	scp -P 20022 HOST_SRC_PATH username@127.0.0.1:DEST_PATH # 把文件从主机复制到容器
    ```

12. git clone 使用 https 地址不需要设置公私玥（使用 SSH 地址时需要）

13. Git

    ```
    1. 初始的全局配置
    	git config --global user.name "Zhang San" # your name
    	git config --global user.email "zhangsan@foo.com" # your email
    	git config --global core.editor vim # your favourite editor
    	git config --global color.ui true
    2. 在没有任何变化的情况下 commit 
    	git commit --allow-empty
    ```

14. **PA0-Acquiring Source Code for PAs-Compiling and Running NEMU 中执行 `make` 出错，提示 `"strcat()" xxxxxx` ，实际并非出错，只是警告，但是 Makefile 文件中指定了 `-Werror` 所以警告全部变成错误，导致编译失败**

    权宜之计：修改 Makefile 文件，将 `-Werror` 删除（其他方法：不提示某些警告，不过失败了，[参考](https://gcc.gnu.org/onlinedocs/gcc-8.3.0/gcc/Option-Index.html#Option-Index)）

15. **PA0-Acquiring Source Code for PAs-Compiling and Running NEMU 中执行 `make run` 出错，提示打开目录失败什么的 ，提示中可以看出 Makefile 企图 `cd /tools/xxxxx` 但是 tools 文件夹位于与 Makefile 相同的层次**

    权宜之计：修改 Makefile 文件，将51行的 `cd $(abspath $(@D)/..) && make` 的改为 `cd .$(abspath $(@D)/..) && make` ，即加一个点

    疑问：照理看，abspath 返回的应该是绝对路径，不知道为什么这里被改变了，没有继续追踪

# 题目解答

1. Why Windows is quite "fat" ?

    Windows 为了强大的兼容性自带了很多驱动程序，占用了大量空间。

    内存方面，好像 W 和 L 都会使用内存做缓存用，不太区分出来占用多少的问题，可能跟机制也有关，严格的进程管理和宽松一点的也有差别。

2. Why do some operations require superuser privilege?

    为了安全。没有权限的用户关闭服务器导致服务器无法提供服务。

3. 消失的 cd

    因为 cd 是 builtin shell command，可以使用 `$ help cd` 或者 `$ man builtins` 查看用法等

    > [参考](https://stackoverflow.com/questions/41147818/no-man-page-for-the-cd-command)

4. Things behind scrolling

    original terminal 不能滚动是因为上下方向键被用来检索输入命令历史了，其实还是可以滚动的，使用的是 `shift + PageUp/PageDown`

    tmux 可以滚动，使用的是 `CTRL+b, PageUp/PageDown` ，需要使用 `ESC` 退出

    没有找到比较靠谱的资料说明 scroll bar 的实现。猜测是事先缓存下来的。

5. Have a try!（主机和容器间复制文件）

    会改变。