# VI

## 基础方法

|function                          |command                 |
|----------------------------------|------------------------|
|打开文本                          |vi test.txt             |
|打开文本（二进制模式）            |vi -b test.txt          |
|进入编辑                          |i                       |
|退出编辑                          |ESC                     |
|退出并修改                        |wq                      |
|退出不修改                        |q!                      |
|复制当前行                        |命令模式下yy            |
|复制n行                           |命令模式下nyy           |
|粘帖                              |命令模式下p             |
|删除当前行                        |命令模式下dd            |
|删除多行(from x to y)             |命令模式下1,10d         |
|删至行首                          |d0                      |
|删至行尾                          |d$                      |
|搜索                              |/keywords  n  shift+n   |
|整页翻页                          | ctrl-f ctrl-b          |
|显示行号                          |:set nu or :set number  |
|光标移至当前行首（注意是数字零）  |0                       |
|光标移至当前行尾                  |$                       |
|跳到档首                          |G                       |
|跳到档尾                          |gg                      |
|跳到240行                         |;240                    |
|撤销上一步                        |u                       |
|恢复上一步                        |ctrl + r                |

## visual block
```
ma // mark as a
ctrl+v // enter block mode
goto another point
shift+i // insert mode
space space space ...
exc // apply to other lines

x delete block
```

## binary file
- vi -b start.vci
- :%!xxd ——将当前文本转换为16进制格式。
- :%!xxd -c 12——将当前文本转换为16进制格式,并每行显示12个字节。
- :%!xxd -r ——将当前文件转换回文本格式。
- :%!od ——将当前文本转换为8进制格式。

## 替换文本
- 替换所有匹配的文本
: %s/str1/str2/g
- 替换每行第一个匹配的文本
: %s/str1/str2/
- 替换当前行所有匹配的文本
: s/str1/str2/g
- 替换当前行第一个匹配的文本
: s/str1/str2/

## 安装vim
yum install vim

## 重定向vi命令为vim
~~~bash
mv /bin/vi vi_bak
ln -s /usr/bin/vim /bin/vi
vi /etc/virc
vi /etc/vimrc
~~~

## 不用空格代替tab
tab宽度
set noexpandtab
set tabstop=4

## 指定编码
:e ++enc=utf-8 myfile.txt

## 忘记sudo了
:w !sudo tee %

## 问题:上下左右键就变成了ABCD了
sudo apt-get install vim-nox

## 中文乱码问题
vi ~/.vimrc

## 解决vim粘贴时格式混乱的问题
如果在.vimrc中设置了自动缩进set autoindent，那么在插入模式下粘贴代码时，vim会自动为代码缩进，导致格式混乱。解决的办法如下
在.vimrc中设置set paste选项，这样粘贴代码时就不会产生缩进了，但是如果需要缩进的时候又要把该选项改回set nopaste。
这样换来换去很麻烦，所以可以设置一个开关。set pastetoggle <F9>
如此，通过按F9键就可以打开和关闭paste选项了，粘贴之前按下F9，需要缩进时再按下F9。

## Windows VIM 中文乱码

~~~bash
C:\Program Files (x86)\Vim\_vimrc
set fileencodings=utf-8,ucs-bom,cp936,big5
set fileencoding=utf-8
~~~

## 去vi搜索后高亮显示

在vi中搜索了一个单词，该单词以高亮显示，看起来很不舒服，怎么能将它去掉在vi的命令模式下输入:nohlsearch就可以了。另外可以在~/.vimrc中写上下面的语句就会有高亮显示：
set hlsearch
加上下面的语句就不会有高亮显示：
set nohlsearch