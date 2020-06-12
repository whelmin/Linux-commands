- [View file content - 查看文件内容](#view-file-content---查看文件内容)
  - [cat](#cat)
  - [tac](#tac)
  - [more](#more)
  - [less](#less)
  - [head](#head)
  - [tail](#tail)
  
## View file content - 查看文件内容

在 Linux 中，我们经常会去看某个文件内容是否更新了，更新了哪些？更改位置在哪里？这时候就需要这些强大的查看文件内容的命令了。

常见的查看文件内容命令：`cat` `tac` `more` `less` `head` `tail` `nl` `od`

### cat

> Concatenate (连续)的简称，将一个文件的内容连续的印出在屏幕上面。

**语法：**

`centos`

```
用法：cat [选项]... [文件]...
将[文件]或标准输入组合输出到标准输出。

  -A, --show-all           等于-vET
  -b, --number-nonblank    对非空输出行编号
  -e                       等于-vE
  -E, --show-ends          在每行结束处显示"$"
  -n, --number             对输出的所有行编号
  -s, --squeeze-blank      不输出多行空行
  -t                       与-vT 等价
  -T, --show-tabs          将跳格字符显示为^I
  -u                       (被忽略)
  -v, --show-nonprinting   使用^ 和M- 引用，除了LFD和 TAB 之外
      --help            显示此帮助信息并退出
      --version         显示版本信息并退出

如果没有指定文件，或者文件为"-"，则从标准输入读取。

示例：
  cat f - g  先输出f 的内容，然后输出标准输入的内容，最后输出g 的内容。
  cat        将标准输入的内容复制到标准输出。
```

`macos` 

```
$ usage: cat [-benstuv] [file ...]
```

### tac

> cat的逆转单词，将一个文件的内容逆序地连续印出在屏幕上面。

**语法：**

同 `cat`

### more

> 按页显示文本内容，可按翻页键一页一页回退

**语法：**

```
$ more $file
```

### less

> 按页显示文本内容，可翻页键一行一行回退

**语法：**

```
$ less $file
```

### head

> 从头开始显示文件指定的行数

**语法：**

```
# 指定显示某文件的前5行
$ head -n 5 $file
```

### tail

> 显示文件指定的结尾的行数

**语法：**

```
# 指定显示某文件的后5行
$ tail -n 5 $file
```

```
用法：tail [选项]... [文件]...
将一个文件的最后10行内容打印在屏幕上面。

  -c, --bytes=K            输出最后K个字节； 或使用-c + K输出从每个文件的第K个字节开始的字节
  -f, --follow[={name|descriptor}] 随着文件的增长输出附加数据； 一个不存在的选项参数表示“描述符”
  -F                       与--follow = name --retry相同
  -n, --lines=K            输出最后的K行，而不是最后的10行； 或者使用-n + K以Kth开头输出
      --max-unchanged-stats=N 使用--follow = name，重新打开在N次（默认5次）迭代后未更改大小的FILE，以查看其是否已取消链接或重命名（这是循环日志文件的常见情况）； 使用inotify时，此选项很少有用
      --pid=PID            使用-f，在进程ID之后终止，PID消失
  -q, --quiet, --silent    从不输出提供文件名的头文件
      --retry              如果无法访问，请继续尝试打开文件
  -s, --sleep-interval=N   使用-f，在两次迭代之间睡眠大约N秒（默认为1.0）； 使用inotify和--pid = P，每N秒至少检查一次进程P
  -v, --verbose            总是输出标头给出文件名
      --help            显示此帮助信息并退出
      --version         显示版本信息并退出

如果您希望即时追查一个文件的有效名称而非描述内容(例如循环日志)，默认
的程序动作并不如您所愿。在这种场合可以使用--follow=name 选项，它会使
tail 定期追踪打开给定名称的文件，以确认它是否被删除或被其它某些程序重新创建过。
```