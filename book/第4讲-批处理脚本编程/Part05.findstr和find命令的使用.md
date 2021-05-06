# 08.findstr和find命令的使用





## find命令

在文件中搜索字符串。

  /N        显示行号
  /I        搜索字符串时忽略大小写。
  /OFF[LINE] 不要跳过具有脱机属性集的文件。
  "string"  指定要搜索的文字串，
  [drive:][path]filename
            指定要搜索的文件。

例：find /i "hello" c:\a.txt

注：在a.txt中查找"hello"并且忽略大小写



## findstr命令的使用

在文件中寻找字符串。

FINDSTR [/B] [/E] [/L] [/R] [/S] [/I] [/X] [/V] [/N] [/M] [/O] [/F:file]
        [/C:string] [/G:file] [/D:dir list] [/A:color attributes] [/OFF[LINE]]
        strings [[drive:][path]filename[ ...]]

  /B        在一行的开始配对模式。
  /E        在一行的结尾配对模式。
  /L        按字使用搜索字符串。
  /R        将搜索字符串作为一般表达式使用。
  /S        在当前目录和所有子目录中搜索
              匹配文件。
  /I        指定搜索不分大小写。
  /X        打印完全匹配的行。
  /V        只打印不包含匹配的行。
  /N        在匹配的每行前打印行数。
  /M        如果文件含有匹配项，只打印其文件名。
  /O        在每个匹配行前打印字符偏移量。
  /P        忽略有不可打印字符的文件。  
  /OFF[LINE] 不跳过带有脱机属性集的文件。
  /A:attr   指定有十六进位数字的颜色属性。请见 "color /?"
  /F:file   从指定文件读文件列表 (/ 代表控制台)。
  /C:string 使用指定字符串作为文字搜索字符串。
  /G:file   从指定的文件获得搜索字符串。 (/ 代表控制台)。
  /D:dir    查找以分号为分隔符的目录列表
  strings   要查找的文字。
  [drive:][path]filename
            指定要查找的文件。

除非参数有 /C 前缀，请使用空格隔开搜索字符串。
例如: 'FINDSTR "hello there" x.y' 在文件 x.y 中寻找 "hello" 或
"there" 。  'FINDSTR /C:"hello there" x.y' 文件 x.y  寻找
"hello there"。

一般表达式的快速参考:
  .        通配符: 任何字符
  *        重复: 以前字符或类别出现零或零以上次数
  ^        行位置: 行的开始
  $        行位置: 行的终点
  [class]  字符类别: 任何在字符集中的字符
  [^class] 补字符类别: 任何不在字符集中的字符
  [x-y]    范围: 在指定范围内的任何字符
  \x       Escape: 元字符 x 的文字用法
  \<xyz    字位置: 字的开始
  xyz\>    字位置: 字的结束

有关 FINDSTR 常见表达法的详细情况，请见联机命令参考。


   findstr参数使用：

   偏移量用法
   findstr /o . 1.txt

   颜色用法
   findstr /a:5c /o . 1.txt

   /A:attr   指定有十六进位数字的颜色属性。请见 "color /?"

   /F:file   从指定文件读文件列表 (/ 代表控制台)

   findstr /f:test.txt /c:"t"

   /G:file   从指定的文件获得搜索字符串。 (/ 代表控制台)。

   findstr /g:1.txt "2.txt"

   /D:dir    查找以分号为分隔符的目录列表

   findstr /d:c:\;d:\ "520hack" 1.txt

  一般表达式举例:

  findstr . 1.txt 或 findstr "." 1.txt  
  从文件1.txt中查找任意字符(包括空格)，不包括空字符或空行(过滤空行)


   findstr .* 1.txt 或 findstr ".*" 1.txt
   从文件1.txt中查找任意字符包括空行(原样打印)

   findstr "[0-9]" 1.txt
   从文件1.txt中查找包括数字0－9的字符串或行


   findstr "[abcezy]" 1.txt
   从文件1.txt中查找包括a b c e z y字母的字符串或行


   finstr "[^0-9]" 2.txt
   任何不在字符集0-9中的字符,即存在字符不属于0-9就打印,
   比如dfd41210   的对方的45  等 就会打印;而54545158将不被打印

   ^和$符号的应用
   ^ 表示行首，"^step"仅匹配 "step hello world"中的第一个单词
   $ 表示行尾，"step$"仅匹配 "hello world step"中最后一个单词

   findstr "[^a-z]" 2.txt
   findstr "[^a-z]" 2.txt
   任何不在字符集a-z中的字符,即存在字符不属于a-z就打印.
   比如adfdfd2225 dfdfdfdfd 等将被打印;而dfdfdffd不被打印

   "\<…\>"这个表达式的作用
    这个表示精确查找一个字符串，\<sss 表示字的开始位置，sss\>表示字的结束位置
    findstr "\<a" 1.txt 精确匹配以字母a开头的行
    findstr "b\>" 1.txt 精确匹配以字母b结尾的行
    findstr "\<ab\>" 1.txt 精确匹配ab字符









## 偏移量用法
findstr /o . %SystemDrive%\boot.ini

颜色用法
findstr /a:5c /o . %SystemDrive%\boot.ini

/f
1.txt text:
%SystemDrive%\boot.ini
findstr /f:c:\1.txt /c:"t" /c:"g"

/d
findstr /d:c:\;d:\ "b" boot.ini


测试搜索的最大字符
@echo off&setlocal ENABLEDELAYEDEXPANSION
for /l %%i in (1,1,160) do (
      set var=!var!1
      findstr /c:"!var!" !SystemDrive!\boot.ini
      echo !var!  %%i
)
pause

1.txt text:
assdf1
ddd
.
fsdfer ft
cccccccccc

.        通配符: 任何字符
findstr . c:\1.txt

*        重复: 以前字符或类别出现零或零以上次数
findstr /r /x /b "d*" c:\1.txt

 ^        行位置: 行的开始
findstr /r /b "^c" c:\1.txt

  $        行位置: 行的终点
findstr "f$" c:\1.txt

[class]  字符类别: 任何在字符集中的字符
findstr  "[cf]" c:\1.txt

[^class] 补字符类别: 任何不在字符集中的字符
findstr  "[^c]" c:\1.txt

[x-y]    范围: 在指定范围内的任何字符a-z A-Z 0-9
findstr  "[1-9]" c:\1.txt

\x       Escape: 元字符 x 的文字用法
findstr  "\." c:\1.txt

\<xyz    字位置: 字的开始
findstr  "\<dd " c:\1.txt

yz\>    字位置: 字的结束

findstr  "t\>" c:\1.txt

findstr  "\<ft\>" c:\1.txt

    