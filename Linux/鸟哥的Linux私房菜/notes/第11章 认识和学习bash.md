bash的优点/功能：

- 命令记忆能力

- 命令和文件补全功能

  Tab接在一串命令的第一个字后面，则为命令补全

  Tab接在一串命令的第二个字后面，则为文件补齐

- 命令别名设置功能

  alias lm = 'ls -al'

- 作业控制、前台、后台控制

- 程序脚本

- 通配符

<br>

type命令：

可以判断命令是来自外部还是bash内嵌的命令。

```
type [-tpa] name
-t: 会用以下字符串表示命令的意义：
	file: 外部命令
	alias: 命令别名
	builtin: 内嵌命令
-p: 如果后面接的是外部命令，才会显示完整文件名
-a: 将由PATH定义的路径中所有含有name的命令都列出来，包括alias
```

<br>

\\[Enter]的用法：

在输入命令后，输入\[Enter]即可执行命令。而输入\\[Enter]后，则会当成换行字符来使用。这样可以将命令分为两行输入

```
[fjx@localhost Desktop]$ type \
> cd
cd 是 shell 内嵌
```

<br>

## Shell中的变量

echo读出变量内容：

```
echo $variable
echo ${variable}

若变量没有被设置，显示内容为空
```

### 变量的设置规则

- 变量设置：**variable=something**

- 等号两边不能直接接**空格**符

- 变量名之内是英文字母和数字，但开头字符不能是数字

- 变量中字符的表示：用**单引号或双引号**括起来

  双引号和单引号的不同点：双引号内的特殊字符，如$，保留原来特性

  单引号内则全为普通字符

- 可以使用**转义字符**[\\]把特殊符号变成一般字符

- 变量指代的字符串中包括命令：**用[\`命令`]或[$(命令)]的形式**

  ```
  var="$(ls -al)"
  echo $var
  ```

- 在变量后面再加内容：

  ```
  var="$var"content
  ```

- 将变量设成环境变量：export variable

- 通常全大写字符为系统默认变量

- 取消变量：**unset** variable

<br>

### 键盘读取、数组和声明

read：读取键盘输入

```
read -[pt] variable
-p: 后接提示符
-t: 后接等待输入的秒数

read -p "input: " -t 30 test
```

<br>

declare/typeset：声明变量的类型

```
declare [-aixr] variable
-a: 数组类型
-i: 整数
-x: 环境变量
-r: readonly类型，该变量不可被更改，也不能重设
```

变量的默认类型是字符串，

bash下的字符运算，默认只做整数运算

<br>

数组类型：

```
var[index]=content
```

<br>

### 变量内容的删除、替代和替换

删除：

```
echo ${path#/*:}
#表示从前向后删除符合匹配的最短字符串，*是通配符。该句的意思是从前向后删除符合以/开头，以:结束的格式的最短字符串。
echo ${path##/*:}
##表示从前向后删除符合匹配的最长字符串。
echo ${path%:*bin}
%表示从后向前删除符合匹配的最短字符串
%%表示从后向前删除符合匹配的最长字符串。
```

<br>

替换：

```shell
${path/sbin/SBIN}	#把第一个sbin替换成SBIN
${path//sbin/SBIN}	#把所有sbin替换成SBIN
```

```shell
username=${username-root}	#username如果不存在，就把username设为root
username=${username:-root}	#username不存在或者空字符串，就把username设为root
```

## 命令别名与历史命令

命令别名：alias

```shell
alias order="oldorder"
unlias order
```

历史命令：history

```shell
history [n]	# 将最近的n条命令列出来
history -c	# 将目前shell中所有history内容全部清除
history -a	# 将目前新增的history命令写入histfiles
history -r	# 将histfiles的内容读到目前这个shell的history中
history -w	# 将目前history写入到histfiles中
```

```shell
!!	# 执行上一条命令
!44 # 执行第44条命令
!al # 执行最近的以al开头的命令
```

## Bash Shell的操作环境

通配符 

| 符号   | 意义                                |
| ---- | --------------------------------- |
| *    | 至少0个字符                            |
| ?    | 一定有一个任意字符                         |
| []   | 一定有一个在中括号内的字符                     |
| [-]  | 代表在编码顺序内的所有字符，如[0-9]代表在0和9之间的所有数字 |
| [^]  | 非，\[^abc]至少有一个字符，且该字符不为abc中的一个    |

其他特殊字符

| 符号     | 意义              |
| ------ | --------------- |
| #      | 注释              |
|       | 转义              |
| \|     | 管道              |
| ~      | 主文件夹            |
| $      | 变量前导符           |
| &      | 作业控制，将命令变成背景下工作 |
| !      | 非               |
| /      | 目录符号，路径分隔符号     |
| \>, >> | 数据流重定向，替换和累加    |
| \<, << | 数据流重定向，输入导向     |
| ' '    | 单引号             |
| “ ”    | 双引号，具有变量置换功能    |
| \` `   | 同$()            |

## 数据流重定向

将某个命令执行后应该要出现在屏幕上的数据传输到其他的地方。

- 标准输入stdin：代码为0
- 标准输出stdout: 代码为1
- 标准错误输出stderr: 代码为2

```
1>: 以覆盖的方式将正确数据输出到指定文件或设备上
1>>: 以累加的方式将正确数据输出到指定文件或设备上
```

将正确信息/错误信息通通写到一份文件中：

```
do do do ... > list 2>&1
do do do ... &> list
```

<br>

输入重定向：

```shell
cat > catfile	# 从键盘输入数据到catfile中
cat > catfile < otherfile	# 将otherfile文件中的数据读入到catfile中
cat > catfile << 'eof'	# 键盘输入数据到catfile中，直到输入eof结束输入
```



<br>

数据重定向常用情况：

- 需要将屏幕输出信息保存下来
- 后台执行程序，不希望干扰屏幕正常的输出结果
- 已知一些命令会输出错误信息，而希望将其丢掉（错误信息写入到'/dev/null'中）
- 错误信息要和正确信息分开输出



<br>

```
cmd ; cmd	前一个命令执行完后紧接着执行下一条命令，两条命令之间没有相关性
cmd && cmd	前一条命令执行正确才执行下一条命令
cmd || cmd	前一天命令执行正确，不执行下一条命令；否则执行下一条命令
```



## 管道命令

管道命令仅能处理标准输入，不能处理stderr

管道命令将前一个命令产生的输出作为输入来处理

cut命令：

在一行信息中截取想要的部分

```
cut -d '分隔字符' -f fields
	-d: 后面接分隔字符
	-f: 后面接数字，表示截取第几段
cut -c 字符范围
	以字符为单位取出固定字符区间

eg: 
export | cut -c 12-
echo $path | cut -d ':' -f 3,5
```

<br>

grep命令：

分析一行信息，如果有所需要的信息，就把该行拿出来。

```
grep [-acinv] [--color=auto] '查找字符串' filename
	-a: 将二进制文件以txt方式查找数据
	-c: 计算查找字符串出现的次数
	-i: 忽略大小写
	-n: 输出行号
	-v: 反向选择，输出没有出现查找字符串的哪一行
```

<br>

sort命令：

排序

```
sort [-fbMnrtuk] [file or stdin]
	-f:忽略大小写
	-b:忽略前面的空格
	-M:以月份排序
	-n:以纯数字排序
	-r:反向排序
	-u:uniq
	-t:分隔符
	-k:以区间进行排序
	
cat /etc/passwd | sort -t ':' -k 3 -n
# 以:为分隔符取第3个区间按数字排序
```

<br>

uniq：将相同的数据仅列出一个显示

```
uniq -i:忽略大小写
uniq -c:计数
```

<br>

wc：计算输出信息的整体数据

```
wc [-lwm]
	-l:仅列出行
	-w:仅列出多少字
	-m:列出多少字符
```

<br>

双向重定向tee：可以将数据流同时送与屏幕和文件。

```
tee [-a] file
-a:以累加的形式
```

<br>

tr：删除和替换文字信息

```
tr [-ds] SET1 ...
-d: 删除字符串
-s: 替换掉重复的字符

last | tr [a-z] [A-Z]
# 将输出信息中所有小写替换成大写
```

col

join：将两汉贴在一起

paste：将两行贴在一起，中间以tab隔开

expand：将tab转换为空格

<br>

split切割：

```
split [-bl] file PREFIX
-b: 后接欲切割成的文件大小，可加单位。
-l: 以行数来切割
PREFIX: 代表前导符，可作为切割文件的前导文字
```

<br>

xargs：参数代换

