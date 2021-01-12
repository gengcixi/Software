从Ubuntu 16.10开始，默认使用dash(theDebian Almquist Shell)而不是bash(the GNUBourne-Again Shell). 但Login Shell还是bash.

 **原因是**dash更快、更高效，而且它符合POSIX规范。Ubuntu在启动的时候会运行很多shell脚本，使用dash可以加快启动速度。

在新写的shell脚本里避免使用**bash的扩展特性**(bashism)

- 使用devscripts包的checkbashisms   命令可以检查shell脚本里是否存在bashism. 
- 安装autoconf-doc包运行info autoconf命令可以阅读"Portable   Shell" 部分的文档来了解POSIX Shell。

举例

- 在"["命令(test)中避免使用-a, -o，应该使用多个"[]"命令并用"&&",   "||"连接。

  ```sh
  ["$foo"="$bar"−a−f/bin/baz"$foo"="$bar"−a−f/bin/baz -o ! -x /bin/quux ]
  ```

  应该替换为：

  ```shell
  ((["$foo" = "$bar" ] && [ -f /bin/baz ]) || [ ! -x/bin/quux ])
  ```

- 不应该使用"[["命令，而应该使用"["命令
- 使用$((…))而不是((…))做算术计算。
- 不能使用$((n++)),   $((--n)) ，而应该是$((n=n+1)) 和$((n=n-1))
- 不要使用{}进行字符扩展，例如/usr/lib/libfoo.{a,so};  
- 避免使用$'…'扩展转义字符。例如，使用"$(printf   '\t')" 代替$'\t'
- 不要使用$"…"进行字符串翻译。应该使用gettext.sh脚本。
- 大部分的${…}进行变量扩展都是可移植的。但是下面的几个不是。
  - ${!...}进行非直接变量扩展，应该使用eval命令。 
  - ${parameter/pattern/string}进行模式替换 
  - ${parameter:offset:length}截取子串

- 不要使用${parm/?/pat[/str]}进行字符替换，而应该使用echo, sed, grep,   awk等命令。

例如：

```shell
OPENGL_VERSION=$(glxinfo| grep "OpenGL version string:")
OPENGL_VERSION=${OPENGL_VERSION/*:/}
```

应该使用：

```shell
OPENGL_VERSION=$(glxinfo| grep "OpenGL version string:" | awk 'BEGIN { FS =":[[:space:]]+" }; { print $2 }')
```

- 不要使用${foo:3[:1]}进行子串切割，使用echo, sed, grep,   awk等命令。

例如：

```shell
string_after="somestring"
string=${string_after:0:3}
```

应该使用：

```shell
string=$(echo$string_after | awk '{ string=substr($0,1, 3); print string; }' )
```

- 在case语句中使用[!]而不是[^]。例如：

```shell
case"foo" in
      [^f]*)
            echo 'not f*'
      ;;
esac
```

替换为：

```shell
case"foo" in
      [!f]*)
		echo 'not f*'
      ;;
esac
```

- dash 不支持$LINENO，虽然它是POSIX标准。
- 不要使用$PIPESTATUS
- 避免使用$RANDOM，而应读取/dev/urandom或者/dev/random。例如：

```shell
random=`hexdump-n 2 -e '/2 "%u"' /dev/urandom`
```

- 一些echo的选项不是portable的，可能其他shell不支持。例如-e, -n
- 函数名前不要加function关键字。
- 不要使用let命令，直接使用=赋值。例如

```
let time=10 和 time=10一样
let time--和time=$((time-1))一样
```

- bash和dash对local关键字的解释不一样。

```shell
local a=5 b=6;  
```

//dash:a和b是全局变量, bash则认为a和b是局部变量。

- 不支持printf %q|%b
- 不要使用select关键字，只有bash才支持。
- source命令也是bash才支持，应该使用'.'命令
- 路径搜索时，`dash` 不支持   `~` 扩展，应该使用$HOME
- 不支持declare 或 typeset
- bash和dash对ulimit和type有不同的选项
- time是bash内置的命令，但是在dash下需要使用time程序
- kill -[0-9] or   -[A-Z]是bash内置的命令
- 在bash里，如果read没有接变量，则会保存在REPLY变量里。在dash应该使用read REPLY替代。
- 不要使用<<<，而是使用<<替代。

例如：

```shell
$cat <<<"$HOME is where the heart is."
/home/ralphis where the heart is.
```

替换为：

```
$cat <<E
\>$HOME is where the heart is.
\>E
/home/ralphis where the heart is.
```

