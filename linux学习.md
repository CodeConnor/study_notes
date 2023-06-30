# Linux学习

[TOC]

## 1、Linux基础命令

命令格式：

```shell
command [-options] [parameters] 
```

绝对路径：从根目录开始

相对路径：从当前目录开始

两种路径贯穿在大多数命令当中

### ls 命令

**查看目录下的文件和文件夹**

- `ls` ：查看当前目录

  `ls /root`：查看指定目录

  `ls /root /home`：同时查看多个目录

- `-a` ：all，所有、

  `ls -a`：all，查看当前目录下隐藏和非隐藏的文件和文件夹

  `ls -a /home`：查看指定目录的所有文件和文件夹

- `-l` ：list，列表显示

  `ls -l` ：可简写为` ll `，以列表形式显示文件和文件夹

  `ls -l /home`：列表形式，指定目录

- `-h` ：显示大小，带单位，必须与`-l`结合使用

  `ls -lh` ：以列表形式显示当前目录下的文件和文件夹，并带单位显示大小



### pwd 命令

**显示当前目录所在的绝对路径**



### cd 命令

**change directory，切换目录**

- `cd`：回到用户家目录

  `cd 目录`：切换到指定目录

  `cd ..` ：回到上一级目录

  `cd -` ：在最近的两个目录间切换



### mkdir 命令

**make directory，创建文件夹**

Linux区分大小写

- `mkdir 文件夹名`：在当前目录下创建

  `mkdir /root/test2`：在绝对路径下创建文件夹

- `-p`：创建前置路径，即递归创建多个层级的文件夹

  `mkdir /test/test1/test2/test3`



### rm 命令

**remove，删除文件或目录**

- `rm a.txt`：删除文件，会有提示

- `-r`：递归，配合rm可删除文件夹

  `rm -r /test`，如果删除的文件夹里有其他文件夹和文件，则会先进入最里的文件夹开始提示是否删除文件

- `-f` ：force，强制，无提示

  `rm -f a.txt` ：强制删除文件且无提示



### touch 命令

**创建空文件**

- `touch 文件名`：当前目录创建

  `touch /root a.txt`：绝对路径创建



### mv 命令

**move，剪切+粘贴，用于文件、目录的移动和重命名**

- `mv a.txt b.txt`：会提示是否覆盖，如果覆盖则是重命名

  无论b.txt不存在或存在，都是重命名

- `mv test1 test2` ：

  当test2存在：即将test1移动到test2中

  当test2不存在：重命名test1

- `mv a.txt test1`：移动文件到指定目录



### cat 命令

**查看文件内容**，输出所有文件内容，适合小文件查看



### more 命令

**查看文件部分内容，按Enter出现一行，按空格出现一页，B返回首页，Q退出**



### less

与more命令相似，不同点在于more查看完所有文件内容后会自动退出文件查看，less需要手动输入q才能退出。



### head

`head`命令用于显示文件的开头部分。它默认显示文件的前10行，但你也可以通过选项来自定义显示的行数。

下面是`head`命令的语法：

```bash
head [选项]... [文件]...
```

常用选项包括：

- `-n`：指定要显示的行数。例如，`head -n 5 file.txt`将显示文件`file.txt`的前5行。
- `-c`：指定要显示的字节数。例如，`head -c 20 file.txt`将显示文件`file.txt`的前20个字节。
- `-q`：不显示文件名。当同时处理多个文件时，使用该选项可以抑制文件名的显示。
- `-v`：始终显示文件名。与`-q`选项相反，该选项会强制显示文件名。

以下是一些示例：

1. 显示文件的前10行：

   ```bash
   head file.txt
   ```

2. 显示文件的前5行：

   ```bash
   head -n 5 file.txt
   ```

3. 显示文件的前20个字节：

   ```bash
   head -c 20 file.txt
   ```

4. 显示多个文件的前10行，并在输出中显示文件名：

   ```bash
   head -v file1.txt file2.txt
   ```



### tail

`tail`命令与`head`命令相反，它用于显示文件的末尾部分。它默认显示文件的最后10行。

- `-n`：指定要显示的行数。例如，`tail -n 5 file.txt`将显示文件`file.txt`的最后5行。
- `-c`：指定要显示的字节数。例如，`tail -c 20 file.txt`将显示文件`file.txt`的最后20个字节。
- **`-f`：监视文件并实时显示新增的内容。适用于查看日志文件等不断更新的文件。**
- `-q`：不显示文件名。当同时处理多个文件时，使用该选项可以抑制文件名的显示。
- `-v`：始终显示文件名。与`-q`选项相反，该选项会强制显示文件名。

监视文件的新增内容：

```bash
tail -f file.txt
```



### cp 命令

**copy，复制+粘贴**

- `cp a.txt b.txt`：将文件内容覆盖

  当b不存在：先创建b，将a的内容复制，然后覆盖到b中

  当b存在：将a的内容覆盖到b中

- -r：复制文件夹，`cp -r test1 test2`：

  当test2存在，将test1文件夹整个复制一份，写入到test2中

  当test2不存在，创建test2，将test1文件夹中的内容复制一份写入到test2中

- `cp a.txt test2`：复制文件写入到文件夹中



### ps 命令

**process status，进程状态**，可查看PID等信息

- `ps -ef`：查看当前正在运行的进程

- uid：进程发起者

  pid：进程ID

  ppid：父进程ID



-- -- -- --

### kill 命令

**终止进程**

- `kill pid`：终止对应PID的进程，不一定能终止，比如终止不了带有保护进程的进程
- `kill -9 pid`：杀死对应进程，一定能杀死进程
- `kill -l`：查看kill命令的所有信号



### ifconfig 命令

**查看虚拟机的网络配置信息**

- windows：ipconfig



### clear 命令

**清屏，快捷键ctrl+l**



### history 命令

查看历史命令，默认1000行



### 重启关机命令

- `reboot`：重启
- `shutdown -h now`：立即关机
- `halt`：不断电关机



### hostname 命令

**查看主机名称**



### tar 命令

**压缩、打包、解包、解压缩**

- `-c`：小写c，打包

- `-v`：view，查看过程

- `-f`：file，打包成指定文件

- `-z`：操作压缩格式的文件，gzip格式

- `-x`：解包，解压缩包

- `-C`：大写C，解包到指定目录

  ```shell
  tar -cvf test1.tar test1   --  将test1文件夹打包成test1.tar文件并查看打包过程
  
  tar -czvf test1.tar.gz test1  -- 打包并压缩
  
  tar -xvf test1.tar -C /bigdata_xiao/test2  -- 解包到指定目录
  
  tar -xzvf test1.tar.gz -C /bigdata_xiao/test3  -- 解压缩包
  ```



### grep 命令

**全文检索命令，可以用于过滤内容和检索关键字**

- `-i`：不区分大小写
- `-r`：递归

```shell
grep 检索关键字 文件路径（文件路径可作为内容输入端口，可通过管道输入内容）

grep hadoop a.txt  -- 在a.txt中检索包含Hadoop的内容

grep -ir hadoop /root  -- 在目标目录中遍历查找包含关键字的内容
```



### 管道命令|

**|：将上一个命令的输入当做下一个命令的输出**

```shell
-- 只要上一个命令有输出，管道都可以将输出结果传给下一个命令的输入

ps -ef | grep mysql  -- 在正在运行的进程中查找mysql
```



### \> 和 >> 命令

在Linux中，`>` 和 `>>` 是重定向操作符，用于将命令的输出重定向到文件中。它们的具体功能如下：

1. `>`：覆盖写入

   - 语法：`命令 > 文件`

   - 功能：执行命令并将输出写入指定的文件。如果文件不存在，则创建新文件；如果文件已经存在，则覆盖文件内容。

   - 示例：

     ```bash
     echo "Hello, World!" > file.txt
     ```

2. `>>`：追加写入

   - 语法：`命令 >> 文件`

   - 功能：执行命令并将输出追加到指定的文件末尾。如果文件不存在，则创建新文件；如果文件已经存在，则将输出追加到文件末尾。

   - 示例：

     ```bash
     echo "Additional text" >> file.txt
     ```

使用这两个重定向操作符，你可以将命令的输出重定向到文件中，以便进行保存、记录或其他处理。请注意，重定向操作符只会将命令的标准输出重定向，不会将标准错误输出重定向。

如果你想将标准错误输出一并重定向到文件，可以使用以下方式：

- 将标准错误输出重定向到文件：

  ```
  命令 2> 错误文件
  ```

- 将标准输出和标准错误输出都重定向到文件：

  ```
  命令 &> 文件
  ```

  或

  ```
  命令 > 文件 2>&1
  ```

其中，`2>` 表示将标准错误输出重定向，`&>` 或 `>` 2>&1` 表示将标准输出和标准错误输出都重定向。



### find

`find` 可用于在指定目录下搜索文件和目录。

`find` 命令的基本语法如下：

```css
find [路径] [表达式]
```

其中，`路径` 指定要搜索的目录路径，可以是相对路径或绝对路径。如果未指定路径，则默认从当前目录开始搜索。

`表达式` 用于指定搜索的条件和操作。下面是一些常用的表达式选项：

- `-name`：按文件名匹配搜索。可以使用通配符（如`*`）进行模式匹配。
- `-type`：按文件类型搜索。可以是`f`（普通文件）、`d`（目录）、`l`（符号链接）等。
- `-size`：按文件大小搜索。可以使用`+`、`-`、`c`（字节）、`k`（KB）、`M`（MB）等进行比较。
- `-mtime`：按文件修改时间搜索。可以使用`+`、`-`进行比较，单位为天。
- `-exec`：执行指定的命令或脚本，对搜索到的文件进行操作。

以下是一些示例：

1. 在当前目录下搜索所有的文本文件：

   ```bash
   find . -name "*.txt"
   ```

2. 在指定目录下搜索文件名以 `file` 开头的文件：

   ```bash
   find /path/to/dir -name "file*"
   ```

3. 在当前目录及其子目录下搜索所有的目录：

   ```bash
   find . -type d
   ```

4. 搜索文件大小大于1MB的文件：

   ```bash
   find . -size +1M
   ```

5. 在当前目录下搜索修改时间在7天以内的文件，并删除它们：

   ```bash
   find . -mtime -7 -exec rm {} \;
   ```



### which 命令

**查看执行命令的位置**



### ln

`ln`命令用于创建链接（link），它可以创建硬链接和符号链接（软链接）。链接是指向文件或目录的引用，可以在文件系统中创建多个链接指向同一个文件或目录，从而实现文件的共享和重用。

`ln`命令的基本语法如下：

```bash
ln [选项] 源文件 目标文件
```

其中，`源文件` 是要链接的文件或目录，`目标文件` 是链接文件或目录的名称。

`ln`命令的常用选项包括：

- `-s`：创建符号链接（软链接）。使用该选项创建的链接是指向源文件的符号链接。
- `-f`：如果目标文件已存在，则强制创建链接，覆盖目标文件。
- `-i`：如果目标文件已存在，询问用户是否覆盖。
- `-n`：禁止解引用目标文件。适用于符号链接，保持链接的原始状态。

以下是一些示例：

1. 创建硬链接：

   ```bash
   ln source.txt link.txt
   ```

   这将在当前目录下创建一个名为 `link.txt` 的硬链接，指向 `source.txt` 文件。

2. 创建符号链接（软链接）：

   ```bash
   ln -s source.txt link
   ```

   这将创建一个名为 `link` 的符号链接，指向 `source.txt` 文件。

3. 创建目录链接：

   ```
   bashCopy code
   ln -s /path/to/source_dir /path/to/link_dir
   ```

   这将创建一个名为 `link_dir` 的符号链接目录，指向 `source_dir` 目录。

4. 强制创建链接，覆盖目标文件：

   ```
   bashCopy code
   ln -sf source.txt link.txt
   ```

   如果 `link.txt` 文件已存在，该命令将强制创建链接，覆盖原有文件。

链接可以用于在不同位置引用同一文件或目录，并且修改一个链接将影响到其他引用该文件或目录的链接。请注意，在创建符号链接时，源文件可以是相对路径或绝对路径。

这只是`ln`命令的一些常见用法示例。你可以通过运行`man ln`命令来查看`ln`命令的完整文档，其中包含更多选项和用法说明。

#### 软链接与硬链接的区别

链接（符号链接）和硬链接是两种不同类型的文件链接。

1. 软链接（Symbolic Link）：
   - 软链接是创建一个指向目标文件或目录的特殊文件。它类似于Windows系统中的快捷方式。
   - 软链接创建一个新的文件，其中包含指向目标文件或目录的路径。软链接文件与目标文件具有不同的 inode 号。
   - 软链接可以跨越不同的文件系统，并且可以链接到不存在的文件或目录。
   - 如果原始文件或目录被删除或移动，软链接将失效，即访问软链接将无法找到目标。
   - 软链接的权限和所有权信息是指向目标文件或目录的。
2. 硬链接（Hard Link）：
   - 硬链接是将一个已存在的文件创建一个新的链接，新的链接与原始文件具有相同的 inode 号。
   - 硬链接只能在同一个文件系统中创建，不能链接到目录，并且不能跨越不同的文件系统。
   - 对于用户来说，通过不同的硬链接或原始文件访问数据没有区别，它们都指向相同的存储位置。
   - 如果原始文件被删除，硬链接仍然保留文件内容，因为硬链接本身指向了相同的数据块。
   - 删除硬链接或原始文件都不会影响其他链接，只有当所有链接都被删除时，文件的存储空间才会被释放。

总结：

- 软链接是一个新的文件，指向目标文件或目录的路径，可以跨越文件系统，但如果目标被删除或移动，软链接失效。
- 硬链接是已存在文件的链接，具有相同的 inode 号，不能跨越文件系统，即使原始文件被删除，硬链接仍然有效。

需要注意的是，使用`ls -l`命令显示链接文件时，软链接的文件类型为`lrwxrwxrwx`，而硬链接的文件类型与目标文件相同。



### vi编辑器

**文本编辑器，只能编辑文本内容，不能进行排版，不支持鼠标操作，没有菜单，只有命令**

- 命令模式：初始进入该模式，有如下命令

  o：在当前行下方插入一空行

  O：在当前行前面插入一空行

  **dd：删除光标所在行**

  ndd：从光标位置向下连续删除 n 行

  **yy：复制光标所在行**

  nyy：从光标位置向下连续复制n行

  **p：粘贴在当前行下一行**

  P：粘贴在当前行上一行

  **u：撤销上一次命令**

  ctrl + r：反撤销

  **gg：回到文件顶部**

  **G：回到文件末尾**

  /str：查找str

  shift + zz：快速保存退出

  注意：使用鼠标从window或者其他地方复制内容到vim编辑器粘贴，一定一定要在输入模式下进行，否则数据会有丢失的风险。

- 插入模式：从命令模式输入“ i、o、O、a、s ”都可以进入该模式，从编辑模式按“ Esc ”进入命令模式

- 命令行模式：从输入模式同时按“shift“ + ” : ”进入该模式，从末行模式按“回车，退格，del”都可以进入命令模式，命令行模式无法直接进入编辑模式

  w：保存

  w 文件名：另存为其他文件名

  q：退出，在没有修改的情况下

  q!：强制退出不保存

  wq：保存退出

![](images\vi键盘图.png)



## 2、Linux用户与权限管理

linux是多用户多任务操作系统，不同用户具有不同操作权限。

用户组是具有相同特征的多个用户的集合。

文件/文件夹归属可分为三类：

拥有者（Owner user）

拥有者所在组（Group user）

其他用户组（Other users）

![文件归属](images\文件归属.png)



### useradd 命令

**创建/添加用户，只能root用户使用**

```shell
useradd 用户名  -- 添加一个普通用户
passwd 用户名  -- 更改用户密码
userdel -r 用户名  -- 删除一个普通用户，不加-r的话删除得不干净
su 用户名  -- 切换用户
```

 

- sudo

  - 功能：给普通用户临时授予root权限。

  - 注意：能够分配sudo的只有root。

  - sudo的配置命令 ==visudo==

  - sudo具体使用

    - step1:使用root用户编辑sudo配置文件

      ```shell
      [root@node1 ~]# visudo
      
      ## Allow root to run any commands anywhere
      root    ALL=(ALL)       ALL
      allen   ALL=(ALL)       ALL
      
      allen   ALL=(ALL)       /usr/bin/ls  #配置只允许执行指定的命令
      ```

    - step2:普通用户执行命令之前需要添加sudo关键字 申请sudo权限校验

      ```shell
      [allen@node1 ~]$ ls /root
      ls: cannot open directory /root: Permission denied
      [allen@node1 ~]$ sudo ls /root
      
      We trust you have received the usual lecture from the local System
      Administrator. It usually boils down to these three things:
      
          #1) Respect the privacy of others.
          #2) Think before you type.
          #3) With great power comes great responsibility.
      
      [sudo] password for allen:    #这里需要输入allen普通用户的密码
      linux02
      [allen@node1 ~]$ sudo ls /root  #密码和sudo校验成功 获取一个为期5分钟的免密操作
      linux02
      ```

---

#### 

### 用户组管理命令

1. groupadd：用于创建新的用户组。

   - 语法：`groupadd [选项] 组名`
   - 示例：`groupadd developers`
   - 选项：
     - `-g GID`：指定新用户组的组标识号（Group ID）。
     - `-r`：创建一个系统用户组。

2. groupdel：用于删除现有的用户组。

   - 语法：`groupdel 组名`
   - 示例：`groupdel developers`

3. groupmod：用于修改现有的用户组的属性。

   - 语法：`groupmod [选项] 组名`
   - 示例：`groupmod -n newname oldname`
   - 选项：
     - `-n 新组名`：修改用户组的名称。
     - `-g 新GID`：修改用户组的组标识号（Group ID）。

4. groups：显示当前用户所属的用户组。

   - 语法：`groups [用户名]`
   - 示例：`groups john`

5. newgrp：切换到一个不同的用户组。

   - 语法：`newgrp 组名`
   - 示例：`newgrp developers`

6. id：显示当前用户的用户标识号（User ID）以及所属的用户组。

   - 语法：`id [用户名]`
   - 示例：`id john`

7. chgrp：`chgrp`命令用于更改文件或目录的所属用户组。

   - 语法：`chgrp [选项] 用户组 文件/目录`
   - 示例：`chgrp developers file.txt`
   - 选项：
     - `-R`：递归地更改目录及其子目录中的文件所属用户组。

   `chgrp`命令主要用于更改文件或目录的所属用户组，而不涉及用户组的切换。只有具有足够权限的用户才能使用`chgrp`命令。

```bash
# 在默认情况下，以下命令通常需要 root 权限（超级用户权限）才能执行：

groupadd：创建新的用户组。
groupdel：删除现有的用户组。
groupmod：修改现有的用户组属性。
newgrp：切换到不同的用户组。
chgrp：更改文件或目录的所属用户组。
```





### chmod 命令

`drwxr-xr-x. 3 root root  33 3月   3 14:02 test1`

| d               | rwx                                 | r-x                 | r-x                     | root   | root   | 33                | 3月   3 14:02 | test1  |
| --------------- | ----------------------------------- | ------------------- | ----------------------- | ------ | ------ | ----------------- | ------------- | ------ |
| 第1列：文件属性 | 第2-4列：创建者对文件或者目录的权限 | 第5-7列：用户组权限 | 第8-10 列：其他用户权限 | 创建者 | 用户组 | 文件大小（Bytes） | 日期时间      | 文件名 |

- 角色

  创建者：一个文件或者文件夹的创建者（拥有者），userid ->  uid -> u

  用户组：针对一个文件或者文件夹而言，默认与创建者同名，groupid -> gid -> g

  其他用户：创建者之外的用户，other -> o

- 权限

  r：read，读权限，r == 4

  w：write，写权限，w == 2

  x：execute，执行权限，x == 1

  没有权限：0

- 权限操作：chmod，change mode

  ```shell
  -- 用字母
  chmod g-w 文件名  -- 对指定文件剥夺用户组的读权限
  chmod g+wx 文件名  -- 对指定文件添加用户组的写和执行权限
  chmod o=rwx 文件名  -- 对指定文件添加所有权限
  
  -- 用数字，使用数字权限时要写三位数字，因为7==007
  chmod 707 文件名 -- 对文件添加创建者和其他用户的所有权限，并剥夺用户组的所有权限
  chmod 777 文件名 -- 对文件添加所有用户的所有权限
  ```

总结：

1. 对于文件来说，×执行权限最高；对于文件夹来说， w权限最高，实际中授权需要谨慎。
2. 权限管理对root用户无约束。主要是针对非root用户来设定的。
3. 通常来说相关性越高，权限越高。正常的话：
   user权限 > group权限 > other权限



## 3、常见系统管理命令

### 时间、日期查看

`date`：查看日期

`cal`：查看日历

### 内存、磁盘使用率查看

`free`：用于显示内存状态。会显示内存的使用情况，包括实体内存，虚拟的交换文件内存，共享内存区段，以及系统核心使用的缓冲区等。
`df`（英文全拼：disk free）：用于显示目前在 Linux系统上的文件系统磁盘使用情况统计

- 选项

  `-h`：人性化显示参数，单位更人性化

  `-s`：间隔执行命令，默认秒

### 进程查看

`ps`：**process status，进程状态**，可查看PID等信息

- `ps -ef`：查看当前正在运行的进程

- uid：进程发起者

  pid：进程ID

  ppid：父进程ID



`jps`：这是JDK自带的命令，专门用于查看本机运行的java进程情况。

## 4、大数据集群环境搭建

### 分布式与集群

分布式系统和集群是计算领域中常用的两个概念，它们有一些区别和联系：

区别：

1. 定义和目标：
   - 分布式系统：分布式系统是由多台独立计算机组成的，它们通过网络进行通信和协调，共同完成一个特定的任务或提供一项服务。分布式系统的目标是将计算任务分散到多台计算机上，以提高性能、可伸缩性和容错性。
   - 集群：集群是由多台计算机（称为节点）组成的，它们通过网络连接在一起，作为一个整体来运行应用程序或服务。集群的目标是通过并行处理和负载均衡来提高性能和可靠性。
2. 系统结构：
   - 分布式系统：分布式系统的计算节点通常是相对独立的，每个节点都可以执行自己的任务，并通过消息传递或共享存储等机制进行通信和协调。
   - 集群：集群中的计算节点通常是相互协作的，它们共享资源和状态，并通过共享存储或共享内存等机制进行通信和同步。
3. 编程模型：
   - 分布式系统：分布式系统中的编程模型通常更加复杂，需要处理分布式计算、数据一致性、消息传递等问题。常见的分布式系统编程模型包括RPC（远程过程调用）、消息队列、分布式文件系统等。
   - 集群：集群中的编程模型相对简化，开发人员可以使用共享内存或分布式共享存储等方式共享数据，编写并行计算任务或使用负载均衡来分配任务。

联系：

1. 多节点：分布式系统和集群都由多个计算节点组成，节点之间通过网络进行通信和协作。
2. 提高性能和可伸缩性：分布式系统和集群都旨在通过将计算任务分散到多个节点上，以提高性能和可伸缩性。
3. 容错性：分布式系统和集群都可以通过冗余和备份机制提供容错能力，使系统在节点故障时继续运行。
4. 并行处理：集群通常用于并行处理大规模的计算任务，而分布式系统则可以用于处理分布式数据、大规模分布式存储等场景。

需要注意的是，虽然分布式系统和集群有一些共同之处，但它们并不是互斥的概念，可以在某些情况下同时使用。例如，一个大规模的分布式系统可以由多个集群组成，每个集群负责不同的子任务。

- 集群架构

  - 主从架构

    ```properties
    主角色:master leader   大哥
    从角色:slave  follower 小弟
    
    主从角色各司其职，需要共同配合对外提供服务。
    常见的是一主多从 也就是一个大哥带着一群小弟共同干活。
    ```

  - 主备架构

    ```properties
    主角色:active
    备角色:standby
    
    主备架构主要是解决单点故障问题的 保证业务的持续可用。
    常见的是一主一备 也可以一主多备。
    ```



### step1 虚拟机克隆

克隆前提：虚拟机要处于关闭状态。

克隆分为：链接克隆、完整克隆，完整克隆意味着两台机器将完全互相独立。完整克隆后两台机器一模一样。但在局域网网络中，有些属性是绝对不能一样的。比如IP、MAC、hostname等。因此需要修改这些冲突的属性。

注意：在真实生产环境里不用虚拟机，而是安装linux系统

### step2 修改ip、hostname

ip：

```bash
vim /etc/sysconfig/network-scripts/ifcfg-ens33

TYPE="Ethernet"     #网卡类型 以太网
BOOTPROTO="none"   #ip等信息是如何决定的？  dhcp动态分配、 static|node 手动静态分配
NAME="ens33"        #网卡名称
ONBOOT="yes"       #是否开机启动网卡服务
IPADDR="192.168.88.152"  #IP地址
PREFIX="24"   #子网掩码   等效: NETMASK=255.255.255.0
GATEWAY="192.168.88.2"  #网关服务
DNS1="192.168.88.2"     #网关DNS解析
DOMAIN="114.114.114.114" #公网DNS解析  114.114.114.114  谷歌：8.8.8.8  阿里百度DNS

只修改“IPADDR”
```

hostname：

```bash
vim /etc/hostname
```

### step3 配置hosts映射

Linux hosts：

```shell
vim /etc/hosts

127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6

192.168.88.151 node1.xiaobang.cn node1
192.168.88.152 node2.xiaobang.cn node2
192.168.88.153 node3.xiaobang.cn node3
```

windows hosts：

```shell
C:\Windows\System32\drivers\etc\hosts

192.168.88.151 node1 node1.xiaobang.cn
192.168.88.152 node2 node2.xiaobang.cn
192.168.88.153 node3 node3.xiaobang.cn
```

### step4 关闭防火墙

firewalld

  ```shell
  #查看防火墙状态
  systemctl status firewalld
  
  #关闭防火墙
  systemctl stop firewalld
  
  #关闭防火墙开机自启动
  systemctl disable firewalld
  
  
  #centos服务开启关闭命令
  centos6:(某些可以在centos7下使用)
  	service 服务名 start|stop|status|restart
  	chkconfig on|off 服务名
  	
  centos7:	
  	systemctl start|stop|status|restart 服务名
  	systemctl disable|enable 服务名  #开机自启动  关闭自启
  ```

selinux

  ```shell
  vim /etc/selinux/config
  
  # This file controls the state of SELinux on the system.
  # SELINUX= can take one of these three values:
  #     enforcing - SELinux security policy is enforced.
  #     permissive - SELinux prints warnings instead of enforcing.
  #     disabled - No SELinux policy is loaded.
  SELINUX=disabled
  ```

需要重启生效

### step5 集群时间同步

背景：分布式软件不同机器不同角色进程之间通常基于时间差来判断彼此角色工作是否正常。

中国处于东八时区，全国时间由国家授时中心发布，叫做北京时间 。

ntp网络时间协议：实现基于网络授时同步时间。

- ntp 网络时间协议 实现基于网络授时同步时间。

- date

  ```shell
  查看当前的系统时间 也可以手动指定设置时间 不精准
  
  [root@node1 ~]# date
  Thu May 20 14:50:30 CST 2021
  ```

- ntpdate

  ```shell
  #ntpdate  授时服务器
  
  ntpdate ntp5.aliyun.com
  
  [root@node1 ~]# ntpdate ntp5.aliyun.com
  20 May 14:53:07 ntpdate[2187]: step time server 203.107.6.88 offset -1.354309 sec
  
  #企业中运维往往不喜欢ntpdate 原因是这个命令同步时间是立即的。不是平滑过渡的。
  ```

- ntpd软件

  ```
  通过配置 平滑的和授时服务器进行时间的同步
  ```

- VMware软件可以让虚拟机的时间和windows笔记本保持一致。

### step6 SSH免密登录

在集群环境中，经常需要在不同机器之间进行跳转，开启免密登录可以提高效率，避免频繁输入密码验证。

此外，免密登录的环境也可以满足通过脚本远程登录各个机器实现各种自动操作，如：一键启动、一键安装等。

免密登录的实现是基于SSH协议实现的。需要打通免密的节点：node1-->node1、node2、node3。

在node1执行命令，打通node1-->node1、node2、node3

```shell
#实现node1----->node2
#step1 在node1生成公钥私钥
ssh-keygen  一顿回车 在当前用户的home下生成公钥私钥 隐藏文件

[root@node1 .ssh]# pwd
/root/.ssh
[root@node1 .ssh]# ll
total 12
-rw------- 1 root root 1675 May 20 11:59 id_rsa
-rw-r--r-- 1 root root  402 May 20 11:59 id_rsa.pub
-rw-r--r-- 1 root root  183 May 20 11:50 known_hosts
#step2
copy公钥给node2
ssh-copy-id node2
注意第一次需要密码

#step3  
[root@node1 .ssh]# ssh node2
Last login: Thu May 20 12:03:30 2021 from node1.itcast.cn
[root@node2 ~]# exit
logout
Connection to node2 closed.

```



### scp远程拷贝

基于SSH协议可以实现同一集群，跨机器间的文件复制操作，这对于分布式软件安装、同步十分重要。

在配置SSH免密登录之后，SCP时就不需要在输入密码验证了，效率更高。

```bash
#本地copy其他机器
scp node1.txt root@node2:/root/
scp -r linux02/ root@node2:$PWD   #copy文件夹 -r参数   $PWD copy至和本机相同当前路径

#为什么不需要输入密码 
因为配置了机器之间的免密登录  如果没有配置 scp的时候就需要输入密码

#copy其他机器文件到本地
scp root@node2:/root/node1.txt  ./  
```

## 5、linux软件安装

### rpm包管理器

rpm是RH系列Linux系统的包管理器（Red-Hat Package Manager），也是RH系列安装的软件包后缀名。

当下这套标准已经扩大成为了行业标准，不仅仅局限于RH系列Linux系统。

rpm操作指的是使用rpm命令进行软件的查看、安装、卸载。

rpm弊端：需要自己提前下载rpm包，手动安装；需要解决rpm包之间的依赖。

### rpm安装mysql

- ==**软件安装目录规范（示例）**==

  ```shell
  /export/server      #软件安装目录
  /export/software    #安装包的目录
  /export/data        #软件运行数据保存的目录
  /export/logs        #软件运行日志
  
  mkdir -p /export/server
  mkdir -p /export/software 
  mkdir -p /export/data
  mkdir -p /export/logs
  ```

> 提示：==MySQL只需要安装在node1服务器即可==。

- 卸载Centos7自带的mariadb

  ```shell
  [root@node3 ~]# rpm -qa|grep mariadb
  mariadb-libs-5.5.64-1.el7.x86_64
  
  [root@node3 ~]# rpm -e mariadb-libs-5.5.64-1.el7.x86_64 --nodeps
  [root@node3 ~]# rpm -qa|grep mariadb                            
  [root@node3 ~]# 
  ```

- 安装mysql

  ```shell
  mkdir /export/software/mysql
  
  #上传mysql-5.7.29-1.el7.x86_64.rpm-bundle.tar 到上述文件夹下  解压
  tar xvf mysql-5.7.29-1.el7.x86_64.rpm-bundle.tar
  
  #执行安装依赖
  yum -y install libaio
  
  [root@node3 mysql]# rpm -ivh mysql-community-common-5.7.29-1.el7.x86_64.rpm mysql-community-libs-5.7.29-1.el7.x86_64.rpm mysql-community-client-5.7.29-1.el7.x86_64.rpm mysql-community-server-5.7.29-1.el7.x86_64.rpm 
  
  warning: mysql-community-common-5.7.29-1.el7.x86_64.rpm: Header V3 DSA/SHA1 Signature, key ID 5072e1f5: NOKEY
  Preparing...                          ################################# [100%]
  Updating / installing...
     1:mysql-community-common-5.7.29-1.e################################# [ 25%]
     2:mysql-community-libs-5.7.29-1.el7################################# [ 50%]
     3:mysql-community-client-5.7.29-1.e################################# [ 75%]
     4:mysql-community-server-5.7.29-1.e################                  ( 49%)
  ```

- mysql初始化设置

  ```shell
  #初始化
  mysqld --initialize
  
  #更改所属组
  chown mysql:mysql /var/lib/mysql -R
  
  #启动mysql
  systemctl start mysqld.service
  
  #查看生成的临时root密码 
  cat  /var/log/mysqld.log
  
  [Note] A temporary password is generated for root@localhost: o+TU+KDOm004
  ```

- 修改root密码 授权远程访问 设置开机自启动

  ```shell
  [root@node2 ~]# mysql -u root -p
  Enter password:     #这里输入在日志中生成的临时密码
  Welcome to the MySQL monitor.  Commands end with ; or \g.
  Your MySQL connection id is 3
  Server version: 5.7.29
  
  Copyright (c) 2000, 2020, Oracle and/or its affiliates. All rights reserved.
  
  Oracle is a registered trademark of Oracle Corporation and/or its
  affiliates. Other names may be trademarks of their respective
  owners.
  
  Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
  
  mysql> 
  
  
  #更新root密码  设置为hadoop
  mysql> alter user user() identified by "hadoop";
  Query OK, 0 rows affected (0.00 sec)
  
  
  #授权
  mysql> use mysql;
  
  mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'hadoop' WITH GRANT OPTION;
  
  mysql> FLUSH PRIVILEGES; 
  
  #mysql的启动和关闭 状态查看 （这几个命令必须记住）
  systemctl stop mysqld
  systemctl status mysqld
  systemctl start mysqld
  
  #建议设置为开机自启动服务
  [root@node2 ~]# systemctl enable  mysqld                             
  Created symlink from /etc/systemd/system/multi-user.target.wants/mysqld.service to /usr/lib/systemd/system/mysqld.service.
  
  #查看是否已经设置自启动成功
  [root@node2 ~]# systemctl list-unit-files | grep mysqld
  mysqld.service                                enabled 
  ```

- Centos7 ==干净==卸载mysql 5.7

  ```shell
  #关闭mysql服务
  systemctl stop mysqld.service
  
  #查找安装mysql的rpm包
  [root@node3 ~]# rpm -qa | grep -i mysql      
  mysql-community-libs-5.7.29-1.el7.x86_64
  mysql-community-common-5.7.29-1.el7.x86_64
  mysql-community-client-5.7.29-1.el7.x86_64
  mysql-community-server-5.7.29-1.el7.x86_64
  
  #卸载
  [root@node3 ~]# yum remove mysql-community-libs-5.7.29-1.el7.x86_64 mysql-community-common-5.7.29-1.el7.x86_64 mysql-community-client-5.7.29-1.el7.x86_64 mysql-community-server-5.7.29-1.el7.x86_64
  
  #查看是否卸载干净
  rpm -qa | grep -i mysql
  
  #查找mysql相关目录 删除
  [root@node1 ~]# find / -name mysql
  /var/lib/mysql
  /var/lib/mysql/mysql
  /usr/share/mysql
  
  [root@node1 ~]# rm -rf /var/lib/mysql
  [root@node1 ~]# rm -rf /var/lib/mysql/mysql
  [root@node1 ~]# rm -rf /usr/share/mysql
  
  #删除默认配置 日志
  rm -rf /etc/my.cnf 
  rm -rf /var/log/mysqld.log
  ```



### yum包管理器

- 介绍

  ```shell
  Yum（全称为 Yellow dog Updater, Modified）是一个在Fedora和RedHat以及CentOS中的Shell前端软件包管理器。基于RPM包管理，能够从指定的服务器自动下载RPM包并且安装，可以自动处理依赖性关系，并且一次安装所有依赖的软件包，无须繁琐地一次次下载、安装。
  ```

- 特点

  - ==自动下载rpm包 进行安装==  前提是联网  不联网就不能用
  - ==解决包之间的依赖关系==

- 原理

  ```shell
  #yum之所以强大原因在于有yum源。里面有很多rpm包和包之间的依赖。
  yum源分为网络yum源和本地yum源。
  
  #其中网络yum源在centos默认集成了镜像地址 只要联网就可以自动寻找到可用的yum源。 前提联网
  #也可以自己搭建本地yum源。实现从本地下载安装。
  ```

- 命令

  ```shell
  #列出当前机器可用的yum源信息
  yum repolist all
   
  #清楚yum源缓存信息
  yum clean all
  
  #查找软件
  rpm list | grep 软件包名称
  
  #yum安装软件   -y表示自动确认 否则在安装的时候需要手动输入y确认下载安装
  yum install -y xx软件名
  yum install -y mysql-*
  
  #yum卸载软件
  yum -y remove 要卸载的软件包名
  ```

- 扩展：Linux上面 ==command  not found== 错误的解决方案。

  ```shell
  #错误信息
  -bash: xxxx: command not found
  
  #原因
  	1、命令写错了
  	2、命令或者对应的软件没有安装
  
  #通用解决方案
  	如果是软件没有安装 
  	yum install -y  xxxx
  	
  	如果上述安装依然无法解决，需要确认命令所属于什么软件
  	比如jps命令属于jdk软件。
  ```

  

### JDK的安装、环境变量配置

- 简单：解压即可使用 但是通常配置环境变量，以便于在各个路径下之间使用java。

- 要求：==**JDK1.8版本**==。

- 步骤

  ```shell
  #上传安装包到/export/server下
  jdk-8u241-linux-x64.tar.gz
  
  #解压到当前目录
  tar zxvf jdk-8u241-linux-x64.tar.gz
  
  #删除红色安装包（可选）
  rm -rf jdk-8u241-linux-x64.tar.gz
  
  #配置环境变量
  vim /etc/profile            #G + o  
  
  export JAVA_HOME=/export/server/jdk1.8.0_241
  export PATH=$PATH:$JAVA_HOME/bin
  export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
  
  
  #重新价值环境变量文件 让配置生效
  source /etc/profile
  
  [root@node1 ~]# java -version      
  java version "1.8.0_241"
  ```

- 将node1的JDK安装包scp给其他机器

  ```shell
   #scp安装包
   cd /export/server/
   scp -r jdk1.8.0_241/ root@node2:$PWD
   
   #scp环境变量文件
   scp /etc/profile node2:/etc/
   
   #别忘了 其他机器source
   source /etc/profile
  ```

## 6、shell编程

### 简单入门

- shell介绍

  - 指的是一种==程序==，往往是使用C语言开发，功能是访问操作系统内核获取操作系统信息。
  - 指的是==shell脚本语言==，使用什么样的命令语法格式去控制shell程序访问内核。
  - 通常情况下，所说shell编程指的shell脚本编程，==学习shell语法规则==。

- shell编程开发规范

  - 在哪里编写？

  ```
  只要能进行文本编辑的地方都可以写  linux上常使用vim编辑器开发
  ```

  - 需要编译？

  ```
  不需要编译
  ```

  - 如何执行？

  ```shell
  需要语法解释器 不需要安装 
  Linux系统中集成了很多个同种类的shell解释器
  
  [root@node1 linux02]# cat /etc/shells 
  /bin/sh
  /bin/bash
  /usr/bin/sh
  /usr/bin/bash
  /bin/tcsh
  /bin/csh
  ```

- 默认shell解释器 ==bash  shell = shell==

  ```
  因为很多linux发行版都以bash作为默认的解释器 所以说市面上大多数shell编程都是基于bash开展的
  
  bash shell免费的。
  ```

- shell的快速入门案例

  - shell脚本文件 后缀名没有要求 ==通常以.sh结尾  见名知意==

  - 格式

    ```shell
    #!/bin/bash   
    echo 'hello shell'
    
    #第一行 指定解释器的路径
    ```

  - 给脚本授予执行权限

    ```
    chmod a+x hello.sh 
    ```

  - 执行shell脚本

    - 绝对路径指定shell脚本

      ```shell
      [root@node1 linux02]# /root/linux02/hello.sh 
      hello shell
      ```

    - 相对路径

      ```shell
      [root@node1 linux02]# hello.sh   #默认去系统环境变量中寻找  错误
      -bash: hello.sh: command not found
      [root@node1 linux02]# ./hello.sh  #从当前目录下找
      hello shell
      ```

    - 把shell脚本交给其他shell程序执行  比如sh

      ```shell
      [root@node1 linux02]# sh hello.sh 
      hello shell
      ```

  - 探讨：后缀名 解释器 执行权限是必须的吗？   不是必须的

    ```shell
    [root@node1 linux02]# vim bye.hs
    echo "bye bye"
    
    [root@node1 linux02]# sh bye.hs 
    bye bye
    
    #文件不是sh结尾 没有授权 没有指定bash解释器路径 但是却可以执行
    #此时这个文件是作为参数传递给sh来执行的  此时解释器是sh 只要保证文件中语法正确就可以执行
    ```

- 扩展：shell 命令、shell 脚本

  - 都是属于shell的东西 
  - shell命令倾向于交互式使用，适合逻辑简单场景
  - shell脚本适合复杂逻辑 理解结合函数、条件判断、流程控制 写出更加丰富的程序。
  - shell命令和shell脚本之间可以互相换行。

  ```shell
  #编写shell脚本 执行脚本
  [root@node1 linux02]# cat hello.sh 
  #!/bin/bash
  echo 'hello shell'
  [root@node1 linux02]# sh hello.sh       
  hello shell
  
  #以shell命令执行
  [root@node1 linux02]# echo 'hello shell'
  hello shell
  ```

### 变量、字符串、反引号、动态传参

- shell变量

  - 语法格式

    ```shell
    变量＝值  #注意等号两边不能有空格
    
    [root@node1 linux02]# name = allen
    -bash: name: command not found
    [root@node1 linux02]# name=allen 
    ```

  - 变量的使用

    ```shell
    [root@node1 linux02]# name=allen  
    [root@node1 linux02]# echo name
    name
    [root@node1 linux02]# echo $name
    allen
    [root@node1 linux02]# echo ${name}
    allen
    [root@node1 linux02]# echo $namewoon
    
    [root@node1 linux02]# echo ${name}woon
    allenwoon
    
    #建议提取变量的时候 使用{}标识变量的边界范围
    
    #unset 删除变量
    #readonly 只读变量  不能修改 相当于java中final修饰的
    
    [root@node1 linux02]# name=allen
    [root@node1 linux02]# echo ${name}
    allen
    [root@node1 linux02]# name=james
    [root@node1 linux02]# echo ${name}
    james
    [root@node1 linux02]# readonly name=allen
    [root@node1 linux02]# echo ${name}       
    allen
    [root@node1 linux02]# name=james         
    -bash: name: readonly variable
    [root@node1 linux02]# unset name
    -bash: unset: name: cannot unset: readonly variable
    
    #只读变量不能够进行删除 只会随着生命周期结束而结束
    #对应shell命令来说 生命周期就是窗口关闭
    #对应shell脚本来说 生命周期就是shell执行结束
    ```

- shell字符串使用

  - 定义字符串

    - 可以使用单引号 可以使用双引号 可以不使用引号
    - ==推荐使用双引号 实现变量的提取==

    ```shell
    [root@node1 linux02]# name=allen
    [root@node1 linux02]# echo $name
    allen
    [root@node1 linux02]# name1='allen1'
    [root@node1 linux02]# echo $name1   
    allen1
    [root@node1 linux02]# name2="allen2" 
    [root@node1 linux02]# echo $name2
    allen2
    
    [root@node1 linux02]# echo my name is ${name}
    my name is allen
    [root@node1 linux02]# echo 'my name is ${name}'
    my name is ${name}
    [root@node1 linux02]# echo "my name is ${name}" 
    my name is allen
    ```

- ==**反引号**==

  - ` 
  - 英文状态下输入ESC下面
  - 功能：表示执行反引号的命令

  ```shell
  #需求：把date命令执行的结果赋值给nowtime变量 
  [root@node1 linux02]# date
  Tue May 18 17:01:55 CST 2021
  [root@node1 linux02]# nowtime=date   #如果没有反引号 理解为字符串
  [root@node1 linux02]# echo $nowtime
  date
  [root@node1 linux02]# nowtime=`date`  #使用反引号 理解为执行命令 把命令的结果进行赋值
  [root@node1 linux02]# echo $nowtime 
  Tue May 18 17:02:41 CST 2021
  ```

#### 动态传参

在执行Shell程序脚本时，可以向shell脚本动态传递参数。好处是某些配置属性不用写死在脚本中。

动态传递参数的方式： 

```shell
./shell程序 [空格] 参数1 [空格] 参数2 ….
```

在shell脚本内部支持语法接收使用变量。

| 动态参数 | 参数含义                                                  |
| -------- | --------------------------------------------------------- |
| $#       | 传递到脚本的参数个数                                      |
| $*       | 以一个单字符串显示所有向脚本传递的参数                    |
| $$       | 脚本运行的当前进程ID号                                    |
| $!       | 后台运行的最后一个进程的ID号                              |
| $@       | 与$*相同,但是使用时加引号,并在引号中返回每个参数.         |
| $?       | 显示最后命令的退出状态.0表示没有错误,其他任何值表明有错误 |

案例：

```shell
#!/bin/bash
echo "第一个参数是：$1"
echo "第四个参数是：$4"
echo "文件名称是：$0"
echo "传递参数的总个数是：$#"
echo "参数列表：$*"

[root@node1 test]# sh practice.sh a1 a2 a3 a4 a5
第一个参数是：a1
第四个参数是：a4
文件名称是：practice.sh
传递参数的总个数是：5
参数列表：a1 a2 a3 a4 a5
```

