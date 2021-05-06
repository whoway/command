# 两大变量


- 批处理中的变量,我把他分为两类,分别为"**系统变量**"和"**自定义变量**"



## 零、常见系统变量记忆

- 我的“用户配置文件”位置——`:\Users\MaxWell`
- 我的Windows系统盘是——`C:`
- 我的Windows盘在的路径——`C:\WINDOWS`
- 最后一个测试，系统变量内部也是忽略大小写的（笔者，要测试这个，是因为笔者学过Linux了，对大小写比较注重！）

```bat

C:\Users\MaxWell>echo %userprofile%
C:\Users\MaxWell

C:\Users\MaxWell>echo %systemdrive%
C:

C:\Users\MaxWell>echo %windir%
C:\WINDOWS

C:\Users\MaxWell>echo %WINDIR%
C:\WINDOWS

C:\Users\MaxWell>
```





## 一、系统变量

系统变量:是系统已经定义好的变量
他们的值由系统根据其事先定义的条件自动赋值,不需要我们来给他赋值,我们只需要调用

要查看这些系统变量,我们可以在CMD里输入set这样就能显示大部分系统变量了.
```bat
set
```



我把他们综合全部列出来!

| 系统变量          | 对应的翻译                                                   |
| ----------------- | ------------------------------------------------------------ |
| %allusersprofile% | 本地，返回“所有用户配置文件”的位置。                         |
| %appdata%         | 本地，返回**默认情况**下“应用程序存储数据”的位置。           |
| %windir%          | 系统，返回操作系统目录的位置。                               |
|                   |                                                              |
| %userprofile%     | 本地 返回当前用户的配置文件的位置。                          |
|                   |                                                              |
|                   |                                                              |
|                   |                                                              |
|                   |                                                              |
|                   |                                                              |
|                   |                                                              |
|                   |                                                              |
|                   |                                                              |
|                   |                                                              |
|                   |                                                              |
|                   |                                                              |
|                   |                                                              |
| %cmdcmdline%      | 本地，返回用来启动当前的 Cmd.exe 的准确命令行。              |
| %comspec%         | %COMSPEC%  			系统 返回命令行解释器可执行程序的准确路径。 |
|                   |                                                              |
|                   |                                                              |
|                   |                                                              |
|                   |                                                              |
|                   |                                                              |
|                   |                                                              |
| %computername%    | 系统 返回计算机的名称。                                      |
| %userdomain%      | 本地 返回包含用户帐户的域的名称。                            |
| %username%        | 本地 返回当前登录的用户的名称。                              |
| %cd%              | 本地 返回当前目录字符串。                                    |



```txt



%CMDEXTVERSION% 	系统 返回当前的“命令处理程序扩展”的版本号。 


%DATE%  			系统 返回当前日期。使用与 date /t 命令相同的格式。由 Cmd.exe 生成。有关 
%ERRORLEVEL%  		系统 返回上一条命令的错误代码。通常用非零值表示错误。 
%HOMEDRIVE%  		系统 返回连接到用户主目录的本地工作站驱动器号。基于主目录值而设置。用户主目录是在“本地用户和组”中指定的。 
%HOMEPATH%  		系统 返回用户主目录的完整路径。基于主目录值而设置。用户主目录是在“本
地用户和组”中指定的。 
%HOMESHARE%  		系统 返回用户的共享主目录的网络路径。基于主目录值而设置。用户主目录是
在“本地用户和组”中指定的。 
%LOGONSERVER%  		本地 返回验证当前登录会话的域控制器的名称。 
%NUMBER_OF_PROCESSORS%  系统 指定安装在计算机上的处理器的数目。 
%OS%  				系统 返回操作系统名称。Windows 2000 显示其操作系统为 Windows_NT。 
%PATH% 				系统 指定可执行文件的搜索路径。 
%PATHEXT% 系统 返回操作系统认为可执行的文件扩展名的列表。 
%PROCESSOR_ARCHITECTURE%  系统 返回处理器的芯片体系结构。值：x86 或 IA64 基于 Itanium 
%PROCESSOR_IDENTFIER% 系统 返回处理器说明。 
%PROCESSOR_LEVEL%  系统 返回计算机上安装的处理器的型号。 
%PROCESSOR_REVISION% 系统 返回处理器的版本号。 

%PROMPT% 本地 返回当前解释程序的命令提示符设置。由 Cmd.exe 生成。 
%RANDOM% 系统 返回 0 到 32767 之间的任意十进制数字。由 Cmd.exe 生成。 
%SYSTEMDRIVE% 系统 返回包含 Windows server operating system 根目录（即系统根目录）的驱动器。 
%SYSTEMROOT%  系统 返回 Windows server operating system 根目录的位置。 
%TEMP% 和 %TMP% 系统和用户 返回对当前登录用户可用的应用程序所使用的默认临时目录。有些应用程序需要 TEMP，而其他应用程序则需要 TMP。 
%TIME% 系统 返回当前时间。使用与 time /t 命令相同的格式。由 Cmd.exe 生成。有关 
time 命令的详细信息，请参阅 Time。 

```




### （1）输出系统变量的值

系统变量,我们如何知道他的值是什么呢?   

用echo

```bat
C:\Users\MaxWell>echo %appdata%
C:\Users\MaxWell\AppData\Roaming

C:\Users\MaxWell>echo %cd%
C:\Users\MaxWell

C:\Users\MaxWell>echo %cmdcmdline%
"C:\WINDOWS\system32\cmd.exe"

C:\Users\MaxWell>echo %comspec%
C:\WINDOWS\system32\cmd.exe

C:\Users\MaxWell>echo %username%
MaxWell

C:\Users\MaxWell>echo %userdomain%
DESKTOP-5B8E7K2

C:\Users\MaxWell>echo %computername%
DESKTOP-5B8E7K2

C:\Users\MaxWell>echo %os%
Windows_NT
```







### （2）批处理返回参数

返回批处理参数

还有一些系统变量，它们是代表一个意思，或者一个操作

分别是`%0 %1 %2 %3 %4 %5 ....到%9`，还有一个`%*`
%0有点特殊，它有几个意思
我们先来说一下%1-%9的意思
%1返回批处理的第一个参数
%2返回批处理的第二个参数
推广：%num 返回批处理的第num个参数

#### %1到%9的测试

例子：
```
rem 保存为test.bat的批处理
@echo off
echo %1 %2 %3 %4 %5
echo %1
echo %2
```

测试：打开CMD，输入test.bat 林俊杰 周杰伦
Tips：注意中间的空格，主要是用来区分各个参数的

```txt
C:\Users\MaxWell>cd Desktop
C:\Users\MaxWell\Desktop>test.bat 林俊杰 周杰伦
林俊杰
周杰伦
请按任意键继续. . .
```

那么这里还有一个%*，它的作用是返回参数而已，不过他是一次返回所有参数的值
例子：

```bat
@echo off
echo %*
```

```txt
C:\Users\MaxWell>cd Desktop
C:\Users\MaxWell\Desktop>test.bat 林俊杰 周杰伦 
林俊杰 周杰伦
请按任意键继续. . .
```


总结：
这些%1和%9可以让批处理也能**带参数运行（很像Linux下gcc -s 啥的）**,**大大提高批处理功能!**

现在我们来讲一下%0这个参数，它有两个意思

#### %0的用处

%0 第一个意思，用%0可以返回批处理所在的绝对路径

例子：
```bat
rem 批处理
@echo off
echo %0
pause
```

效果:它会把批处理所在的路径给显示出来了
```txt
"C:\Users\MaxWell\Desktop\test.bat"
请按任意键继续. . .
```

#### %0 第二个意思

就是用它来无限循环执行批处理程序

（注意，此死循环只在充cmd中不断输出，可以手动停止执行，可以直接测试）
例子：
```bat
rem 批处理
@echo off
net user
%0
```


保存为BAT执行,他就会无限循环执行net user这条命令,直到你手动停止.

原理解释：当我们把这个%0加到批处理的最后一行,
这样当他执行时,就把再次执行一次原批处理文件,因为%0返回的是当前批处理的绝对路径
比如当前批处理路径为d:\test.bat,那我们把%0加到最后,也就等于在最后面加了一句d:\test.bat,
这样原BAT就会再次被执行.(批处理中只要填入文件绝对路径就会执行它)




#### 其他东西
举个实际例子,比如我们要复制文件到当前帐号的启动目录里就可以这样
copy d:\1.bat "%USERPROFILE%\「开始」菜单\程序\启动\"
%USERPROFILE% 返回当前登录用户的主目录。  注意有空格的目录要用引号引起来,上一节课有说明.
这些变量名,重新启动后也会存在,并不会消失,我们能不能创建这样不会消失的系统变量呢?
可以,使用setx 命令就可以了
setx test 我是值
这样我们就建立了一个重新启动也不消失的变量,setx命令只有2003系统才有.

以上系统变量只是返回一些具体的值

举例说明：
copy c:\h.bat "%USERPROFILE%\「开始」菜单\程序\启动\"
%USERPROFILE%是一个系统变量，表示的值可通过上面介绍的方法来查看
注意那个""符号，因为目录中含有空格。所以这个符号不能少。

以上系统变量只是返回一些具体的值








## 二、自定义变量

自定义变量：提供给用户使用的就是用户自己定义的变量。


故名思意,自定义变量就是由我们来给他赋予值的变量
要使用自定义变量就得使用set命令了,看例子.



### （1）类似python中的变量定义

```bat
rem 批处理
@echo off
set var=我是变量值
echo %var%
pause
```

测试

```txt
我是变量值
请按任意键继续. . .
```

var为变量名,=号右边的是要给变量的值
这就是最简单的一种设置变量的方法了






### （2）用户输入变量值-交互式

变量的值由我们运行后自己用键盘输入!

例子:（注意：var变量名  =号右边的是提示语,不是变量的值）
```bat
rem 批处理，set /p 参数的使用
@echo off
set /p var=请输入变量的值：
echo %var%
pause
```

测试
```txt
请输入变量的值：麦克斯韦
麦克斯韦
请按任意键继续. . .
```

