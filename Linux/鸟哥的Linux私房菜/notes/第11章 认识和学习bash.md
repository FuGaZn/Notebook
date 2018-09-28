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

变量的设置规则：

- 变量设置：**variable=something**

- 等号两边不能直接接**空格**符

- 变量名之内是英文字母和数字，但开头字符不能是数字

- 变量中字符的表示：用**单引号或双引号**括起来

  双引号和单引号的不同点：双引号内的特殊字符，如$，保留原来特性

  单引号内则全为普通字符

- 可以使用**转义字符**[\\]把特殊符号变成一般字符

- 变量指代的字符串中包括命令：用[\`命令`]或[$(命令)]的形式

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

键盘读取、数组和声明

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

