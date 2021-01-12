# 2>/dev/null和>/dev/null 2>&1和2>&1>/dev/null的区别         

#### 一、区别：

**2>/dev/null**
 意思就是把错误输出到“黑洞”

**>/dev/null 2>&1**
 默认情况是1，也就是等同于1>/dev/null 2>&1。意思就是把标准输出重定向到“黑洞”，还把错误输出2重定向到标准输出1，也就是标准输出和错误输出都进了“黑洞”

**2>&1 >/dev/null**
 意思就是把错误输出2重定向到标准出书1，也就是屏幕，标准输出进了“黑洞”，也就是标准输出进了黑洞，错误输出打印到屏幕

参考链接：https://blog.csdn.net/longgeaisisi/article/details/90519690

# shell 字符串判断

------

字符串的判等应该使用「=」或「==」符号；

数字的判等才是使用「-eq」来进行

------

## shell 判断字符串是否为空

正确做法：

```sh
#!/bin/sh 
STRING= 
if [ -z "$STRING" ]; then   
  echo "STRING is empty"    
fi 
if [ -n "$STRING" ]; then   
  echo "STRING is not empty"    
fi
```

  输出结果：

```sh
root@james-desktop:~# ./zerostring.sh    
STRING is empty
```

------

错误做法：

```sh
#!/bin/sh 
STRING= 
if [ -z $STRING ]; then   
  echo "STRING is empty"    
fi 
if [ -n $STRING ]; then   
  echo "STRING is not empty"    
fi 
```

 输出错误结果：

```sh
root@james-desktop:~# ./zerostring.sh    
STRING is empty    
STRING is not empty
```

------

## 判断字符串是否以某个字符(串)开头、包含、结尾

```sh
# 以字符串开头判断
#!/bin/bash
# set -x

var="ixyzero.com is the best!"

function func_main() {
	# if [ $# -gt 0 ]; then
	# 	input="$1"
	# else
	# 	input="ixyzero.com"
	# fi
	input=${1:-"ixyzero.com"}
	echo $input
	
	# echo ${#input}	# ${#input} 是 $input 变量的长度
	if [ ${var:0:${#input}} = $input ]; then
		echo "\"$var\" startwith $input"
	else
		echo "\"$var\" not startwith $input"
	fi
}
func_main "$@"
```

```sh
# 以字符串结尾判断
#!/bin/bash
# set -x

var="ixyzero.com is the best!"

function func_main() {
	# if [ $# -gt 0 ]; then
	# 	input="$1"
	# else
	# 	input="ixyzero.com"
	# fi
	input=${1:-"best!"}
	echo $input
	
	# echo ${#input}	# ${#input} 是 $input 变量的长度
	if [ ${var:0-${#input}} = $input ]; then
		echo "\"$var\" endwith $input"
	else
		echo "\"$var\" not endwith $input"
	fi
}
func_main "$@"
```

```sh
# 字符串包含判断
# returns OK if $1 contains $2
strstr() {
  [ "${1#*$2*}" = "$1" ] && return 1
  return 0
}
```

