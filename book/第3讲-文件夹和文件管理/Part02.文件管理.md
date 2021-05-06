

# 第3讲-Part02.文件管理



> 命令清单
> | 命令                   | 作用                                                        |
> | ---------------------- | ----------------------------------------------------------- |
> | type                   | 显示文本文件的内容                                          |
> | copy                   | 将一份或多份文件复制到另一个位置                            |
> | del                    | 删除一个或数个文件                                          |
> | move                   | 移动文件并重命名文件和目录。(Windows XP Home Edition中没有) |
> | ren                    | 重命名文件                                                  |
> | attrib                 |                                                             |
> | Assoc(Association)命令 |                                                             |






## （1）type
学完下面这个type命令，你就可以知道文件里写了什么东西。 

```bat
type　文件名
```

比如说，我想知道abc.txt文件的内容，就从键盘上输入`type　abc.txt  `    

Tips：提醒你一下，除了文件扩展名是txt的文件，，对其它文件你最好不要使用type命令，否则屏幕上可能会出现很多怪模怪样的符号，还会嘀嘀地乱叫，弄得你心烦意乱。    

Reason：计算机底层原理，我们在C语言中知道主要宏二进制和文本文件，所以是编码的原因！非计算机方向的读者不需要深究。






## （2）copy
copy在英文中是复制的意思，所谓复制就是原来的文件并没有任何改变，将一个或多个文件从一个位置复制到其他位置,重新产生了一个内容和原来文件没有任何差别的文件。PS：拷贝文件和复制文件是没有任何区别的，拷贝是copy的音译。


### 1、在**当前目录**下

复制“原文件.bat”一份，并且重命名为“新文件.old”

```git
copy　原文件.bat　新文件.old
```



### 2、copy命令使用通配符进行多个文件拷贝

copy命令也可以使用通配符

例如要复制F盘中上所有以k开头的所有文件

```bat
copy　F:\k*.* C:\Users\MaxWell\Desktop
```



复制当前目录下所有扩展名是cpp的文件

```bat
C:\Users\MaxWell\Desktop>copy *.cpp F:\
solve.cpp
test.cpp
        2 file(s) copied.

C:\Users\MaxWell\Desktop>copy *.cpp D:
solve.cpp
test.cpp
        2 file(s) copied.
        
C:\Users\MaxWell\Desktop>copy F:\*.xmind C:\Users\MaxWell\Desktop
F:\Windows命令行9讲.xmind
F:\标准函数库.xmind
        2 file(s) copied.

C:\Users\MaxWell\Desktop>
```

如何想要学习高阶用法，请自行学习计算机方向内容《正则表达式》





### 3、某目录下的文件复制到某目录下

```bat
C:\Users\MaxWell\Desktop>md 111

C:\Users\MaxWell\Desktop>md 222

C:\Users\MaxWell\Desktop>copy solve.cpp ./111
The syntax of the command is incorrect.

C:\Users\MaxWell\Desktop>copy solve.cpp .\111
        1 file(s) copied.

C:\Users\MaxWell\Desktop>cd 111

C:\Users\MaxWell\Desktop\111>dir
 Volume in drive C is OS
 Volume Serial Number is 8C53-D31E

 Directory of C:\Users\MaxWell\Desktop\111

12/17/2020  04:00 PM    <DIR>          .
12/17/2020  04:00 PM    <DIR>          ..
12/16/2020  09:31 PM               153 solve.cpp
               1 File(s)            153 bytes
               2 Dir(s)  63,359,418,368 bytes free

C:\Users\MaxWell\Desktop\111>
```

命令格式：copy  C:\520hack.txt  D:\   (将c:\520hack.txt复制到d:\)

### 4、路径的注意事项

路径中如果有空格的话就会出现错误，假设有：

```bat
copy  C:\Documents demo\test.txt  D:\
```


会得不到正确结果。如何解决呢？

**给路径加双引号**，即

```bat
copy  "C:\Documents demo\test.txt"  D:\
```





### 5、实用HK小技巧

 可以通过copy命令将图片和一个文件放在一起

```git
copy /b 1.jpg+1.txt 2.jpg	
```







## （3）del



del即delete（删除）的缩写，删除文件,要删除当前目录中的某个文件，输入del空格再加上文件名就可以了。


```bat
del　文件名.bat
```



### del支持通配符

要删除一类文件，可以使用通配符。

例如del　*.tmp，就是把所有扩展名是tmp的文件都删除。



删除某个目录中的所有文件，注意：只删除目录中的文件，不删除目录！！！！

```bat
C:\Users\MaxWell\Desktop\111>dir
 Volume in drive C is OS
 Volume Serial Number is 8C53-D31E

 Directory of C:\Users\MaxWell\Desktop\111

12/17/2020  04:09 PM    <DIR>          .
12/17/2020  04:09 PM    <DIR>          ..
12/16/2020  09:31 PM               153 solve.cpp
12/16/2020  09:31 PM               153 test.cpp
               2 File(s)            306 bytes
               2 Dir(s)  63,356,403,712 bytes free

C:\Users\MaxWell\Desktop\111>cd ..

C:\Users\MaxWell\Desktop>del 111
C:\Users\MaxWell\Desktop\111\*, Are you sure (Y/N)? Y

C:\Users\MaxWell\Desktop>dir
 Volume in drive C is OS
 Volume Serial Number is 8C53-D31E

 Directory of C:\Users\MaxWell\Desktop

12/17/2020  04:11 PM    <DIR>          .
12/17/2020  04:11 PM    <DIR>          ..
12/17/2020  04:16 PM    <DIR>          111
——————省略——————————————
               4 File(s)      1,608,537 bytes
               4 Dir(s)  63,356,436,480 bytes free
```



## 



````bat
del命令有几个重要的参数：

  /P            删除每一个文件之前提示确认。
  /F            强制删除只读文件。
  /S            从所有子目录删除指定文件。
  /Q            安静模式。删除全局通配符时，不要求确认。
````



例：
如果你要删除c盘下所有的`demo.txt`，且文件demo.txt是只读的，该怎么办呢？

```bat
del /f /s  c:\demo.txt	
```





### 实战——垃圾处理

```bat
@echo off
echo 正在清除系统垃圾文件，请稍后。。。
del /s /f /q %systemdrive%\*.tmp >nul 2>nul
del /s /f /q %systemdrive%\*.gid >nul 2>nul
del /s /f /q %systemdrive%\*.chk >nul 2>nul
del /s /f /q %systemdrive%\*.old >nul 2>nul
del /s /f /q "%userprofile%\local settings\temp\*.*" >nul 2>nul
del /s /f /q "%userprofile%\recent\*.*" >nul 2>nul
del /s /f /q "%userprofile%\cookies\*.*" >nul 2>nul
del /s /f /q "%userprofile%\local settings\history\*.*" >nul 2>nul
del /s /f /q "%windir%\temp\*.*" >nul 2>nul
del /s /f /q "%windir%\prefetch\*.*" >nul 2>nul
echo 垃圾文件清理完毕!
echo. & pause
```





## （4）move

```git
　　move 　　　 移动文件，改目录名　 
［适用场合］　　移动文件到别的目录 
［用　　法］　　move [文件名] [目录]　　　　　　　 移动文件至新目录下 
　　　　　　　　move [目录名] [目录名] 　　　　　　改目录名 
［例　　子］　　c:\>move c:\autoexec.bat c:\old? 
　　　　　　　　移动autoexec.bat文件至old目录下 
　　　　　　　　c:\>move c:\config.sys c:\temp? 
　　　　　　　　移动config.sys文件至old目录下 
```

将C:\Test\1.txt移动到D盘根目录。（相当于剪切）

```git
move  C:\Test\1.txt  D:\
```

当前文件夹有两个东西，一个叫demo的文件夹，一个叫demo.txt的文件
可以这样把demo文件剪切到demo文件夹中去

```git
move demo.txt .\demo
```








## （5）ren(Rename)
     如果想给一个文件改个名字，可以用ren(rename）命令。ren命令的格式是：ren　源文件名 目的文件名。
　　例如把abc.txt改成bne.dat

```git
ren　abc.txt　bne.dat
```

注意：如果用ren命令更改非当前目录中的文件名，那么源文件名和目的文件名要在同一个目录内。 
命令格式:

```bat
Ren c:\1.exe c:\2.exe 
```

 将C盘下的1.exe改名为2.exe





## （6）Attrib(Attribute)

```git
显示、设置或删除指派给文件或目录的只读、存档、系统以及隐藏属性。如果在不含
参数的情况下使用，则 attrib 命令会显示当前目录中所有文件的属性
字符信息含义:+(设置属性)  -(清除属性)   R(Read)[只读文件属性]   A(Archive)[存档文件属性]
              S(System)[系统文件属性]   H(Hide)[隐藏文件属性]
+r 设置文件只读属性
-r 去除文件只读属性
attrib *.*                (查看某文件的属性)
attrib +s +h notepad.exe  (设置文件系统、隐藏属性)
attrib /s +r +h *.exe     (设置当前目录以及子目录下所有后缀为.exe的文件属性)
```







## （7）assoc(Association)

```bat
命令格式:
Assoc - 显示文件系统中扩展名的关联信息
Assoc .后缀名 － 显示此后缀名的关联信息
Assoc .后缀名=某个关联信息 － 修改此后缀名的关联信息
```



测试

```bat
C:\Users\MaxWell\Desktop>dir
 Volume in drive C is OS
 Volume Serial Number is 8C53-D31E

 Directory of C:\Users\MaxWell\Desktop

12/17/2020  03:05 PM    <DIR>          .
12/17/2020  03:05 PM    <DIR>          ..
——————————————省略——————————
12/16/2020  09:31 PM               153 solve.cpp
12/16/2020  09:31 PM         1,608,038 solve.exe
——————————————省略——————————
               7 File(s)      1,807,932 bytes
               2 Dir(s)  63,360,385,024 bytes free

C:\Users\MaxWell\Desktop>assoc solve.cpp
File association not found for extension solve.cpp

C:\Users\MaxWell\Desktop>assoc solve.exe
File association not found for extension solve.exe
```



## （8）cat

cat的含义是concatenate，也就是“连结”