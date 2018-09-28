# <center>CentOS
<br>

GNOME界面，资源管理器Nautilus<br>
KDE界面，资源管理器Konqeror


在Linux中，英文大小写字母是不一样的。

Linux下命令格式：<br>
command [-options] parameter1 parameter2 ...

## 基础命令:


date：显示时间<br>

```
date +%Y/%m/%d  ## 2018/8/10
date +%H:%M ## 20:17
```

cal：显示日历<br>
格式： cal [[mouth] year]<br>


bc：计算器<br>
bc默认输出整数，如果需要输出小数，需要定义小数位数：scale=number<br>
退出bc环境：quit

<br>

命令行模式下执行命令，有两种主要情况：
- 直接显示结果，回到命令提示符等待下一个命令的输入
- 进入该命令的环境，直到结束该命令才回到命令提示符



## 重要的热键
### Tab
Tab键具有“命令补全”和“文件补齐”的功能。
<br>
- Tab接在一串命令的第一个命令后面，则为命令补全<br>
- 接在一串命令的第二个命令后面，则为文件补齐

举例：
- ca \[tab][tab] 输出所有以ca开头的命令
- ls -al ~/.bash\[tab][tab]  输出所有以.bash开头的文件名

### [Ctrl]-c
中断目前程序

### [Ctrl]-d
代表键盘输入结束，可以替代exit的功能

## man page & info page
man command就可以查看这个命令的相关操作说明
<br>
按下/后，光标会移动到最底下一行，这时可以输入关键字来查询<br>

info page:<br>
和man page一下子输出一堆信息不同，info page则是将文件数据拆成一个一个的段落，每个段落用自己的页面来撰写，并且在各个页面中还有类似网页的“超链接”来跳到不同的页面中，每个独立的页面被称为节点(node)

## 文本编辑器nano
用nano打开文件：nano text.txt

[Ctrl]-G取得在线帮助<br>
[Ctrl]-X离开<br>
[Ctrl]-O保存文件<br>
[Ctrl]-W查询<br>

## 正确关机
sync命令：将数据写入硬盘。在关机或重启前，应该多执行几次<br>

shutdown

| 命令   | 意义           |
| ---- | ------------ |
| -t   | 后加秒数，“过几秒关机” |
| -k   | 发送警告信息，不真关机  |
| -r   | 服务停止后重启      |
| -h   | 服务停止后关机      |
| ...  | ...          |

除此之外，还要在命令后面加上时间

| 命令                        | 意思                                    |
| ------------------------- | ------------------------------------- |
| shutdown -h now           | 立即关机                                  |
| shutdown -h 20:25         | 系统在今天20:25关机，若在21:25执行该命令，则在隔天20:25关机 |
| shutdown -h +10           | 十分钟后自动关机                              |
| shutdown -r now           | 立即重启                                  |
| shutdown -r +30 "message" | 30分钟重启，在此之前显示后面的消息给所有在线的用户            |
| shutdown -k now "message" | 不关机，但会发送警告信件                          |

