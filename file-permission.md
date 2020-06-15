- [File permission - 设置文件和目录的访问权限](#file-permission---设置文件和目录的访问权限)
  - [一、查看文件的访问许可权限](#一查看文件的访问许可权限)
  - [二、改变文件的访问许可权限](#二改变文件的访问许可权限)
    - [2.1 使用到的命令](#21-使用到的命令)
    - [2.2 访问者用如下标识来区分](#22-访问者用如下标识来区分)
    - [2.3 访问权的修改方式](#23-访问权的修改方式)
    - [2.4 例子](#24-例子)
  - [三、附录](#三附录)
    - [3.1 如何查看用户和用户组](#31-如何查看用户和用户组)
## File permission - 设置文件和目录的访问权限

在 linux 系统中，每个文件和目录都有访问许可权限，访问权分为 `可读`、`可写`、`可执行` 三种，访问者分为 `用户权限`、`用户组权限`、`其他权限`、`所有人权限` 四种。


### 一、查看文件的访问许可权限

我们在桌面新建一个文件，看其默认的访问许可权限是什么

```
# 新建 hello.py

touch hello.py
```

通过 `ll` 可以查看到该文件的访问许可权限

```
-rw-r--r--   1 whelmin  staff     0B  6 12 15:52 hello.py
```

其中 `-rw-r--r--` 共 10 位，第一位代表`文件类型`（`-`为文件类型、`d` 为文件夹/目录类型），第二位到第四位代表 `用户权限`、第五位到第七位为 `用户组权限`、第八位到第十位为 `其他权限`。

上面表示 `hello.py` 的权限为当前用户可读可写不可执行、用户组可读不可写不可执行、其他权限可读不可写不可执行。

### 二、改变文件的访问许可权限

#### 2.1 使用到的命令

- `chmod` 改变文件或目录的访问权限

- `chown` 改变文件或目录的拥有者

#### 2.2 访问者用如下标识来区分

- `u`，用户（user）    
- `g`，用户组（group）
- `o`，其他（other）   
- `a`，所有（all）  

#### 2.3 访问权的修改方式

访问权的标识

- `r` 可读，权限值为 **4**
- `w` 可写，权限值为 **2**
- `x` 可执行，权限值为 **1**

- `+{code}`，增加某个权限
- `-{code}`，删除某个权限
- `={code}`，赋予给定权限，并取消其他所有的权限

> code 为访问权标识，即 r、w、x

#### 2.4 例子

1. **让 hello.py 可被当前用户执行**

```
chmod u+x hello.py
```

修改成功了：
```
-rwxr--r--   1 whelmin  staff     0B  6 12 15:52 hello.py
```

2. **让 hello.py 可被所有用户可读可写**

```
chmod a+r+w-x hello.py
```

修改成功了：
```
-rw-rw-rw-   1 whelmin  staff     0B  6 12 15:52 hello.py
```

3. **让 hello.py 可被所有用户不可读不可写不可执行**

```
chmod a-r-w-x hello.py
```

修改成功了，但用户依然可以可读可写：
```
-rw-------   1 whelmin  staff     0B  6 12 15:52 hello.py
```

### 三、附录

#### 3.1 如何查看用户和用户组

**常用命令**

* 适用于 macOS 和 linux 系统的命令

- `whoami`，查看当前用户
- `groups`，查看所有的用户组
- `groups ${user}`，查看指定用户所在用户组
  
    ![如何查看用户和用户组示意](/images/20200614231122.jpg)

* 只适用于 macOS 系统的命令，`dscl`
  
> dscl 是 directory services command line （目录服务命令行）的简称。

- `dscl . -list /groups`，查看所有组
- `dscl . -list /users` ，查看所有的用户
- `dscl . -list /groups PrimaryGroupID`，查看所有组和组ID
- `dscl . -list /users UniqueID`， 查看所有的用户和用户ID
- `dscl . -read /groups/admin` ，查看指定组 admin 的详细信息
- `dscl . -read /groups/admin GroupMembership` ，查看指定组 admin 的所有成员

补充对用户和用户组的增删改：

- `dscl . -create /groups/g_whelmin`，创建用户组，名字为 g_whelmin
- `dscl . -delete /groups/g_whelmin`，删除用户组，名字为 g_whelmin
- `dscl . -create /users/u_whelmin`，创建用户，名字为 u_whelmin
- `dscl . -delete /users/u_whelmin`，删除用户，名字为 u_whelmin
- `dscl . -append /groups/g_whelmin GroupMembership u_whelmin`，将 u_whelmin 用户加入指定的用户组 g_whelmin 
- `dscl . -delete /groups/g_whelmin GroupMembership u_whelmin`，将 u_whelmin 用户从指定的用户组 g_whelmin 删除

![使用 dscl 查看用户和用户组示意](/images/20200615112852.jpg)

**存放路径**

- `/etc/passwd`，用户的存放位置
- `/etc/group`，用户组的存放位置