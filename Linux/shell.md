## Shell中的特殊变量说明

~~~
变量	说明
$$	Shell本身的PID（ProcessID）
$!	Shell最后运行的后台Process的PID
$?	最后运行的命令的结束代码（返回值）
$-	使用Set命令设定的Flag一览
$*	所有参数列表。如"$*"用「"」括起来的情况、以"$1 $2 … $n"的形式输出所有参数。
$@	所有参数列表。如"$@"用「"」括起来的情况、以"$1" "$2" … "$n" 的形式输出所有参数。
$#	添加到Shell的参数个数
$0	Shell本身的文件名
$1～$n	添加到Shell的各参数值。$1是第1参数、$2是第2参数…。
~~~

## 调试脚本

~~~
sh -x test.sh
~~~

## get script directory

~~~
$( cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd )"
~~~
