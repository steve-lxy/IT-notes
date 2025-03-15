## Moving Cursor

### Basic Moving

```
h left; j down; k up; l right
```

### Moving in the current line

```
0 to the beginning
$ to the end
^ to the first non-blank character
```

### Moving by words

```
w to the start of the next word
e to the end of a word
b to the start of a word
```

> Using capital letters of the above will ignore punctuations.

### Moving by sentences

```
) to the next sentence
( to the previous sentence
```

### Moving by paragraphs

```
{ to the next paragraph
} to the previous paragraph
```

### Moving

```
H 移动到屏幕的顶部
M 移动到屏幕的中间
L 移动到屏幕的最后
```

### 以屏幕为单位的移动

```
^F 向下移动一屏
^B 向上移动一屏
^D 向下移动半屏
^U 向上移动半屏
```

### 移动到文件末尾：G

### 执行重复次数：在命令前面键入数字以重复执行后面的命令

Sample: 3{ // 向后移动3个段落

> 对于以屏幕为单位的移动，如果设置了数字，后面继续调用该命令时一直会使用这个数字。

### 跳转到前一位置

```
`` 连续两个反引号跳转到前一位置
'' 连续两个单引号跳转到前一位置所在行的开头
```

### 跳转到标记位置

```
m 开头后跟一个字母以标记一个位置
` 反引号后跟这个字母以跳转到标记时的位置
' 单引号后跟这个字母以跳转到标记行的开头
```

### 搜索模式

/regex	向下搜索指定的正则表达式

/		  向下重复搜索前一正则表达式

?regex	向上搜索指定的正则表达式

? 		向上重复搜索前一正则表达式

n		重复上一条/或?命令，搜索方向相同

N		重复上一条/或?命令，搜索方向相反



### 使用行号

行号关闭情况下，可以通过^G查看光标所在行的行号。

:set number 打开行号显示选项

nG 或 :n 跳转到第n行

gg  或 1G 或 :1  跳转到编辑缓冲区的第一行

G 或 :$ 跳转到编辑缓冲区的最后一行

## 插入文件

以下命令都将vi改变到输入模式

i 在当前光标位置前插入数据

a 在当前光标位置后插入数据

I 在当前行开头处插入数据

A 在当前行末尾处插入数据

o 在当前行下面插入一行

O 在当前行上面插入一行

<Esc> 返回到命令模式



## 修改文本

r 精确替换1个字符（不进入输入模式）

R 以覆盖方式替换

s 以插入方式替换1个字符

C 以插入方式从当前光标处替换到这一行的末尾

cc 或 S 以插入方式替换当前的整行

cmove 以插入方式从当前光标处替换到move（移动光标的命令）所给出的位置处

Sample:

```
cw // 替换一个单词
c) // 从当前位置开始替换到段落的末尾
c6} // 替换6个段落
```



## 替换文本

```
:s/pattern/replace/ // 在当前行上以replace替换第一个pattern，最后一个/可以省略
:s/pattern/replace/g // 在当前行上以replace替换所有pattern
:s/pattern/replace/c // 替换之前手工确认
:5s/pattern/replace // 替换第5行的
:8,10s/pattern/replace // 替换从第8行至第10行中的
:.,$s/pattern/replace/g // 替换从当前行起至缓冲区最后一行的所有
:1,.s/pattern/replace/g // 替换从缓冲区第一行至当前行的所有
:%c/pattern/replace/g // 替换缓冲区中所有行的
```

手工确认替换结果时，可^C停止命令执行。

## 反转字母的大小写

~ 反转光标当前字母的大小写，不会改变非字母字符

100~ 从当前光标开始将本行后100个字符反转，命令不会跨越行尾

## 分隔与连接行

分行：将光标移动到待分隔单词后的空格处，然后键入: r<Return>

接行：J，将下一行接到本行

## 删除文本

x	删除当前光标处的字符

X	删除光标左边的字符

D	删除从当前光标到本行末尾的字符

dmove 删除从当前光标到move所给位置的字符，所以，dG删除当前行到缓冲区末尾的所有行，dgg删除从当前行到缓冲区开头的所有行

dd	删除当前行

:lined 删除指定行

:line1,line2d 删除指定范围的行

## 撤销或重复改变

u 撤销上一条命令对编辑缓冲区的修改

U 恢复光标当前行所作的所有修改

.  重复上一命令对编辑缓冲区的修改

## 恢复删除的行

每当删除一行或多行文本时，vi都将删除内容保存在一个特殊的存储区中——编号缓冲区(numbered buffer)，编号从1至9。任何时候都可以将一个编号缓冲区中的内容插入到编辑缓冲区中。

用法：键入一个"（双引号）后面跟缓冲区编号，后面再跟一个p（在当前行下面插入）或P（在当前行上面插入）

Tip：可以u命令撤销，以.命令重复并将编号自动加一，所以，当记不得具体编号时，可用"1pu.u.u这样的命令序列迅速尝试。

## 移动文本

vi总是在无名缓冲区(unnamed buffer)中为上一次删除保存一份副本，在任何时候都可以用p(在其后)或P(在其前)命令将其中的内容复制到编辑缓冲区。

xp 调换两个字符

deep 调换两个单词（光标开始处位于第一个单词的左边）

ddp 调换两行

## 复制文本

使用y、yy或Y命令将文本由编辑缓冲区复制到无名缓冲区中，成为接出(yank)。

yw 接出1个单词

yb 向上（往回）接出1个单词

y2) 接出2个句子

y5} 接出5个段落

yy 接出1行

10yy 接出10行

## 复制与移动行

通过指定行号来复制或移动行

```
:x[,y]coz // 将源行（x，或x至y）复制到目标行(z)的下面
:x[,y]mz // 将源行（x，或x至y）移动到目标行(z)的下面
```

Sample:

```
:1,.m$ // 将第1行至当前行之间的行移动到编辑缓冲区的末尾
:.,$m0 // 将当前行至最后一行的内容移动到编辑缓冲区的开头
```

## 输入shell命令

不停止vi调用shell命令

```
:!date // 调用date命令，回车后返回vi
:!! // 调用上一条shell命令
:sh // 启动一个新的shell以输入多条命令
```

## 将shell命令的输出插入编辑缓冲区

```
:r !program // 在当前行后插入程序program的输出
:liner !program // 在指定行lien后插入程序program的输出
```

## 将文件中的数据插入编辑缓冲区

```
:r file // 在当前行后插入文件file的内容
:liner file // 在指定行line后插入文件file的内容
```

## 使用程序处理数据

```
n!!program // 从当前行开始，在n个行上执行程序program
!move program // 从当前行至move行执行程序program
```

Sample:

```
5!!sort // 将后面5行排序
先使用gg命令跳转到首行，然后!Gsort // 将整个编辑缓冲区排序
```

## 将数据写入文件

除ZZ命令外，还可以使用：

```
:w 将数据写入原始文件
:w file 将数据写入到一个新文件中
:w! file 覆盖一个已有的文件
:w>>file 将数据追加到指定文件中
:10,20w>>file 将第10至20行追加到指定文件中
```

## 刷新屏幕：^L

## 设置选项

```
:set [no]option... // 设置开关选项，如:set number / :set nonumber
:set option[=value]... // 设置变量，如:set ts=4
```

| 开关       | 缩写 | 默认值 | 含义                                        |
| ---------- | ---- | ------ | ------------------------------------------- |
| autoindent | ai   | off    | 和shift width相关，缩进以匹配上一行/下一行  |
| autowrite  | aw   | off    | 如果文本已经修改，则在切换文件前保存        |
| errorbells | eb   | off    | 当显示错误消息时发出嘀嘀声                  |
| exrc       | ex   | off    | 在当前目录中查找初始化文件                  |
| ignorecase | ic   | off    | 在搜索过程中忽略大小写                      |
| list       | --   | off    | 将制表符显示为^I，将行尾显示为$             |
| number     | nu   | off    | 显示行号                                    |
| readonly   | ro   | off    | 不允许修改编辑缓冲区的内容                  |
| showmatch  | sm   | off    | 输入模式：显示匹配的(){}[]                  |
| showmode   | smd  | off    | 当进入输入模式时显示一个提醒                |
| wrapscan   | ws   | off    | 在搜索过程中，环绕到文本的开头/末尾继续搜索 |

| 变量       | 缩写 | 默认值 | 含义                          |
| ---------- | ---- | ------ | ----------------------------- |
| lines      | --   | 24     | 文本的行数（窗口/屏幕大小-1） |
| shiftwidth | sw   | 8      | autoindent使用的空格数量      |
| tabstop    | ts   | 8      | 制表符间距                    |
| wrapmargin | wm   | 0      | 设置自动换行时的页边距(0=off) |

```
:set all // 显示所有选项的值
:set number? // 显示特定选项的值
:set // 显示所有改变了默认值的选项
```

