# 	if命令的详细介绍

<font style="background: yellow">类似于C语言，批处理也有它的语句结构。</font>


批处理的语句结构主要有选择结构(if语句)、循环结构(for语句)等。
  if语句实现条件判断，包括字符串比较、存在判断、定义判断等。
	通过条件判断，if语句即可以实现选择功能。


## 1、字符串比较
    if语句仅能够对两个字符(串)是否相同、先后顺序进行判断等。其命令格式为：
IF [/I] [not] string1 compare-op string2 command1 [else command2]
    其中，比较操作符compare-op有以下几类：
== - 等于
EQU - 等于	equal
NEQ - 不等于	Not equal
LSS - 小于	less
LEQ - 小于或等于	
GTR - 大于	greater
GEQ - 大于或等于
    选择开关/i则不区分字符串大小写；
    选择not项，则对判断结果进行逻辑非。
    字符串比较示例：


```bat
@echo off
set str1=abcd1233
set str2=ABCD1234
if %str1%==%str2% (echo 字符串相同！) else (echo 字符串不相同！)
if /i %str1% LSS %str2% (echo str1^<str2) else (echo str1^>=str2)
echo.
set /p choice=是否显示当前时间？(y/n)
if /i not %choice% EQU n echo 当前时间是：%date% %time%
pause>nul
（测试可以）-------------（像上面这个IF语句一样，if后和else后的语句集用（）括起来是蛮好的！！！值得学习）
```
    对于最后一个if判断，当我们输入n或N时的效果是一样的，都不会显示时间。
    如果我们取消开关/i，则输入N时，依旧会显示时间。
    另外请注意一下几个细节：1-echo str1^<str2和echo str1^>=str2；2-echo.。
    （其中第一处，^应该是转义？？第二处，echo.是打印一行空的？？）



2、存在判断 （exist n.存在！！！）
    存在判断的功能是判断文件或文件夹是否存在。其命令格式为：
IF [NOT] EXIST filename command1 [else command2]
@echo off
if exist %0 echo 文件%0是存在的！
if not exist %~df0 (
echo 文件夹%~df0不存在！
) else echo 文件夹%~df0存在！
pause>nul
（测试可以）
    这里注意几个地方：
    1-存在判断既可以判断文件也可以判断文件夹；
    2-%0即代表该批处理的全称(包括驱动器盘符、路径、文件名和扩展类型)；
    3-%~df0是对%0的修正，只保留了其驱动器盘符和路径，详情请参考for /?，属高级批处理范畴；（？？？？）
    4-注意if语句的多行书写，多行书写要求：
   command1的左括号必须和if在同一行、
   else必须和command1的右括号同行、
   command2的左括号必须与else同行、
   command1和command2都可以有任意多行，
   即command可以是命令集。



3、定义判断  （defined 定义！！！）
    定义判断的功能是判断变量是否存在，即是否已被定义。其命令格式为：
IF [not] DEFINED variable command1 [else command2]
    存在判断举例：
```bat
@echo off
set var=111
if defined var (echo var=%var%) else echo var尚未定义！
set var=
if defined var (echo var=%var%) else echo var尚未定义！
pause>nul
（测试可以）
    对比可知，"set var="可以取消变量，收回变量所占据的内存空间。





一、if的三种用法

IF [NOT] ERRORLEVEL number command
IF [NOT] string1==string2 command
IF [NOT] EXIST filename command

(1)、IF [NOT] ERRORLEVEL number do something
ERRORLEVEL number是错误码也称返回码。（只是这么叫而已，和错误二字没必然联系。）
如果最后运行的程序返回一个错误码（返回码），如果它等于或大于指定数字number，则指定条件为 true。

例子：
```bat
@echo off
ipconfig
if errorlevel 1 goto a
if errorlevel 0 goto b
:a
echo 结果为a!
pause
exit
:b
echo 结果为b!
pause
解释：“ipconfig”执行成功，则返回码为0
```
这种用法现在很少用了,因为他需要使用到CHOICE命令,
这个命令现在被set /p代替了,他是判断CHOICE命令选择的
选项的. CHOICE命令是一个提供选项功能的命令.

例子:

```bat
@echo off
CHOICE /c ab 
if ERRORLEVEL 2 goto bb
if ERRORLEVEL 1 goto aa
:aa
echo 您选择了 a 
goto end
:bb
echo 您选择了 b 
goto end

:end
pause
%0
```

这个用法现在我们一般把他变通一下用,用来判断上一条件命令是执行成功,还是执行失败了.
一般上一条命令的执行结果代码只有两结果,"成功"用0表示  "失败"用1表示.

举个例子:
```bat
@echo off
net user
IF %ERRORLEVEL% == 0 echo net user 执行成功了!
pause
```

这种判断错误的语法是我自己加的,%ERRORLEVEL%这是个系统变量,
返回上一条命令的执行代码("成功"用0表示  "失败"用1表示.)

上面这是判断命令执行成功的,再来一个判断命令执行失败的.

@echo off
net usertest
IF %ERRORLEVEL% == 1 echo net user 执行失败了!
pause

这个是判断上一条命令是否执行失败的

现在我们来一个综合应用的.
@echo off
set /p var=随便输入个命令: 
%var%
if %ERRORLEVEL% == 0 goto yes
goto no
:yes
echo %var% 执行成功了
pause
exit
:no
echo 基本上执行失败了..
pause

这个是根据你输入的命令,自动判断是成功还是失败了!

在来一个简化版的,顺便把把if命令的缩写语法介绍了!
@echo off
set /p var=随便输入个命令: 
%var%
if %ERRORLEVEL% == 0 (echo %var%执行成功了) ELSE echo %var%执行失败了!
pause

else后面写上执行失败后的操作!

当然我门还可以把if else这样的语句分成几行写出来,使他看上去好看点... 
 这也是IF命令的一种缩写语法
@echo off
set /p var=随便输入个命令: 
%var%
if %ERRORLEVEL% == 0  (
   echo !var! 执行成功了
   ) ELSE (
   echo 基本上执行失败了..
   )
pause

刚才介绍的两种IF缩写语法很有用,后面的代码我都用缩写语法,这可以减少代码量.


(2)、IF [NOT] string1==string2 do something
如果指定的文字字符串匹配，指定条件为 true。
例：
@echo off
if "520hack" == "520hack" echo 我们相等!
pause 

当然，也可以用于字符串变量的比较，如下：
@echo off
set str1=520hack
set str2=520hack
if %str1% == %str2% echo 我们相等!
pause

这里去掉两个变量的值，在加个/p来理解这个参数的作用吧!


这个呢就是用来比较变量或者字符的值是不是相等的.
例子
@echo off
set /p var=请输入第一个比较字符: 
set /p var2=请输入第二个比较字符: 
if %var% == %var2% (echo 我们相等) ELSE echo 我们不相等
pause

上面这个例子可以判断你输入的值是不是相等,但是
你如果输入相同的字符,但是如果其中一个后面打了一个空格,
这个例子还是会认为相等,如何让有空格的输入不相等呢?我们在比较字符上加个双引号就可以了.
@echo off
set /p var=请输入第一个比较字符: 
set /p var2=请输入第二个比较字符(多输入个空格试试): 
if "%var%" == "%var2%" (echo 我们相等) ELSE echo 我们不相等
pause



(3)、IF [NOT] EXIST filename do something
这个就是判断某个文件或者文件夹是否存在的语法
如果指定的文件名存在，指定条件为 true。
例:
@echo off
if exist mstsc.exe echo 当前目录下存在文件mstsc.exe
pause 

解说：如果当前文件夹下存在mstsc.exe则显示“当前目录下存在文件mstsc.exe”，否则不显示。

以上各句中的[NOT]是可选项，表示只有条件为 false 的情况下，才应该执行该命令。

例子
@echo off
if exist "c:\test" (echo 存在文件) ELSE echo 不存在文件
pause
判断的文件路径加引号是为了防止路径有空格,如果路径有空格加个双引号就不会出现判断出错了!


二、if-else语句
ELSE 子句必须在 IF 之后出现在同一行上。
例：
@echo off
IF EXIST a.txt (del a.txt) ELSE echo 不存在文件!
pause

解说：如果存在文件a.txt则删除，否则显示“不存在文件!”。本程序段的这种写法是ELSE 子句在 IF 之后出现在同一行上的特殊形式，它是通过括号“(”和“)”相连接的。

由于 ELSE 命令必须与 IF 命令的尾端在同一行上，以下子句不会有效:

IF EXIST a.txt del a.txt
ELSE echo a.txt 不存在文件!

因为 del 命令需要用一个新行终止，以下子句不会有效:
IF EXIST a.txt del a.txt ELSE echo 不存在文件!
需要用括号扩上。
IF EXIST a.txt (del a.txt) ELSE echo 不存在文件!

三、if的嵌套用法
例:
@echo off
set /p var=请输入一个数字：
if %var% gtr 5 if %var% lss 10 echo 这是一个大于5小于10的数!
pause
解说：首先要注意“%var%”，若要取出变量的值要用%%将变量括起来。其次运算符gtr代表大于，lss代表小于，类似的运算符还有：
	 EQU - 等于
 	 NEQ - 不等于
 	 LSS - 小于
 	 LEQ - 小于或等于
  	 GTR - 大于
  	 GEQ - 大于或等于

我几举一个例子,大家都懂数学...不讲多了
@echo off
set /p var=请输入一个数字: 
if %var% LEQ  4 (echo 我小于等于4) ELSE echo 我不小于等于4
pause

最后我们展示一个让系统重启指定次数的BAT,使用IF命令来进行判断

@echo off
:让系统可以重新自动启动三次
copy %0 "%USERPROFILE%\「开始」菜单\程序\启动\" /y
if not  EXIST c:\1 echo.>c:\1&shutdown /r /t 30&exit 
if not  EXIST c:\2 echo.>c:\2&shutdown /r /t 30&exit 
if not  EXIST c:\3 echo.>c:\3&shutdown /r /t 30&exit 


综合实例：
@echo off
:again
s=
cls
color f
set /p p=please input password:
set s=520hack
  if "%p%"=="%s%" (
      echo 您已经通过了认证!&start cmd.exe
  ) else (
      echo 密码错误!
  )
pause >nul
goto again






另外IF还有一些增强的用法,如下
  IF [/I] string1 compare-op string2 command
  IF CMDEXTVERSION number command
  IF DEFINED variable command

IF CMDEXTVERSION,我不做介绍,因为他和上面的if errorlevel用法表示的意义基本一样,只简单说说  
IF [/I] string1 compare-op string2 command 这个语句在判断字符时不区分字符的大小写
还有 IF DEFINED variable command

先说IF [/I] string1 compare-op string2 command 
看这两个例子


@echo off
if a == A (echo 我们相等) ELSE echo 我们不相等
pause
执行后会显示我们不相等

@echo off
if /i a == A (echo 我们相等) ELSE echo 我们不相等
pause

加上/I不区分大小写就相等了!


我们再来看IF DEFINED variable command   这是我们论坛一位版主示例代码.
```bat
:: if defined xxx 是判断xxx是否被定义为变量名的
@echo off
set num=abc
:: 这时num被定义为变量名,而abc是变量num的值
:: 所以以下会显示num ok,因为num被定义了.
if defined num (echo num ok) else echo num no
pause
:: 此时abc未被定义,也就是说还没有abc这个变量名,
:: 而变量num的值是abc,所以这句if是判断num的值是否被定义,而不是判断num是否被定义.
if defined %num% (echo abc ok) else echo abc no
pause
:: 如下:将abc定义一下,结果就不同了.
set abc=hhh
if defined %num% (echo abc ok) else echo abc no
pause
```

