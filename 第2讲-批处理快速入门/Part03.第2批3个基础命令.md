# 第2讲-Part03.第2批3个基础命令



</br>

## （1）start 命令

调用外部程序，所有的DOS命令和命令行程序都可以由start命令来调用。

如：`start calc.exe` 即可打开Windows的计算器

常用参数： 

> min 开始时窗口最小化 
> SEPARATE 在分开的空间内开始 16 位 Windows 程序 
> HIGH 在 HIGH 优先级类别开始应用程序 
> REALTIME 在 REALTIME 优先级类别开始应用程序 
> WAIT 启动应用程序并等候它结束 
> parameters 这些为传送到命令/程序的参数 
> 执行的应用程序是 32-位 GUI 应用程序时，CMD.EXE 不等应用程序终止就返回命令提示。
> 如果在命令脚本内执行，该新行为则不会发生。

请测试下面的程序，会发现神奇现象:smiley:

```bat
C:\Users\MaxWell>start . rem 以默认大小将窗口打开

C:\Users\MaxWell>start /min . rem 以最小化窗口打开

C:\Users\MaxWell>start /max . rem 以最大化窗口打开


```




笔者常用

```bat
:: 打开当前文件夹
start .
```



</br>

</br>

## （2）goto 命令

- 从单词命令会知道，可能是“跳转”命令

- 更显然的，C语言程序员显然会知道这是跳转

在批处理中允许以“`:XXX`”来构建一个标号，然后用GOTO XXX跳转到标号:XXX处，然后执行标号后的命令。标签的名字可以随便起，但是最好是有意义的字符串啦，前加个冒号用来表示这个字符串是标签，goto命令就是根据这个冒号（:）来寻找下一步跳到到那里。最好有一些说明这样你别人看起来才会理解你的意图。

测试下面批处理:smile_cat:

```bat
@echo off
:start
set /a var+=1
echo %var%
if %var% leq 3 GOTO start
pause
```

```txt
运行显示：
1
2
3
4
```





</br>

## （3）call

- 本命令，经常在“**批处理脚本文件**”中出现！！！

CALL命令可以在批处理执行过程中调用另一个批处理，当另一个批处理执行完后再继续执行原来的批处理



```txt
调用一条批处理命令，和直接执行命令效果一样，特殊情况下很有用，比如变量的多级嵌套，见教程后面。
在批处理编程中，可以根据一定条件生成命令字符串，用call可以执行该字符串，见例子。  
CALL [drive:][path]filename [batch-parameters]  
调用的其它批处理程序。filename 参数必须具有 .bat 或 .cmd 扩展名。
CALL :label arguments
调用本文件内命令段，相当于子程序。被调用的命令段以标签:label开头
以命令goto :eof结尾。
另外，批脚本文本参数参照(%0、%1、等等)已如下改变:
批脚本里的 %* 指出所有的参数(如 %1 %2 %3 %4 %5 ...)
批参数(%n)的替代已被增强。您可以使用以下语法:（看不明白的直接运行后面的例子）
%~1         - 删除引号(")，扩充 %1
%~f1        - 将 %1 扩充到一个完全合格的路径名
%~d1        - 仅将 %1 扩充到一个驱动器号
%~p1        - 仅将 %1 扩充到一个路径
%~n1        - 仅将 %1 扩充到一个文件名
%~x1        - 仅将 %1 扩充到一个文件扩展名
%~s1        - 扩充的路径指含有短名
%~a1        - 将 %1 扩充到文件属性
%~t1        - 将 %1 扩充到文件的日期/时间
%~z1        - 将 %1 扩充到文件的大小
%~$PATH : 1 - 查找列在 PATH 环境变量的目录，并将 %1扩充到找到的第一个完全合格的名称。
如果环境变量名未被定义，或者没有找到文件，此组合键会扩充到空字符串可以组合修定符来取得多重结果:
%~dp1       - 只将 %1 扩展到驱动器号和路径
%~nx1       - 只将 %1 扩展到文件名和扩展名
%~dp$PATH:1 - 在列在 PATH 环境变量中的目录里查找 %1，并扩展到找到的第一个文件的驱动器号和路径。
%~ftza1     - 将 %1 扩展到类似 DIR 的输出行。
在上面的例子中，%1 和 PATH 可以被其他有效数值替换。%~ 语法被一个有效参数号码终止。%~ 修定符不能跟 %*使用注意：
```



参数扩充时不理会参数所代表的文件是否真实存在，均以当前目录进行扩展要理解上面的知识，下面的例子很关键。

（下面这个测试批处理，收集自网络资源，侵删:smile:）


```bat
@echo off
Echo 产生一个临时文件 > tmp.txt
Rem 下行先保存当前目录，再将c:\windows设为当前目录
pushd c:\windows
Call :sub tmp.txt
Rem 下行恢复前次的当前目录
Popd
Call :sub tmp.txt
pause
Del tmp.txt
exit
:sub
Echo 删除引号： %~1
Echo 扩充到路径： %~f1
Echo 扩充到一个驱动器号： %~d1
Echo 扩充到一个路径： %~p1 
Echo 扩充到一个文件名： %~n1
Echo 扩充到一个文件扩展名： %~x1
Echo 扩充的路径指含有短名： %~s1 
Echo 扩充到文件属性： %~a1 
Echo 扩充到文件的日期/时间： %~t1 
Echo 扩充到文件的大小： %~z1 
Echo 扩展到驱动器号和路径：%~dp1
Echo 扩展到文件名和扩展名：%~nx1
Echo 扩展到类似 DIR 的输出行：%~ftza1
Echo.
Goto :eof
```

例：

```bat
set aa=123456
set cmdstr=echo %aa%
call %cmdstr%
pause
```

本例中如果不用call，而直接运行%cmdstr%，将显示结果%aa%，而不是123456



</br>

### 用法1：批处理程序之间的调用

先分别保存下面的`1.bat`和`2.bat`到同一个目录下，然后双击1.bat观察现象！

```bat
rem 请将这个文件保存为1.bat
@echo off
echo 本文件（1.bat）显示的内容
call 2.bat
pause
```



```bat
rem 请将这个文件保存为2.bat
@echo off
echo 我是第2个文件，我叫2.bat
```



</br>

### 用法2：call参数的使用

先分别保存下面的`3.bat`和`4.bat`到同一个目录下，然后双击`3.bat`观察现象！

```bat
rem 请将这个文件保存为3.bat
@echo off
echo 我是3号bat文件
call 4.bat one two
pause
```



```bat
rem 请将这个文件保存为4.bat
@echo off
echo %1 %2
```



</br>

### 用法3：call增强参数的使用

先分别保存下面的`5.bat`和`6.bat`到同一个目录下，然后双击`5.bat`观察现象！

```bat
rem save as 5.bat
@echo off
echo 555555555555
call 6.bat HACV

pause
```



```bat
rem 请将这个文件保存为6.bat
@echo off
echo %1
echo %~1
```



</br>

### 用法4：子程序的调用

子程序例1.bat

```bat
@echo off
call :sub return 你好

echo 子程序返回值：%return%
pause

:sub
set %1=%2

goto :eof
```



子程序例2.bat

```bat
@echo off
call :sub sum 10 20 50

echo 运算的结果：%sum%
pause >nul

:sub
set /a %1=%2+%3+%4

goto :eof
```

