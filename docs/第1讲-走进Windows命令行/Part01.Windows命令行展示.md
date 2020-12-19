## 第1讲-Part01.Windows命令行展示



> 小提示：
>
> 如果你是一个毫无Windows命令行经验的读者，接下来
>
> 请你和我这样做，你将打开命令行的大门:smile:



## 一、Windows命令行输出“Welcome”

### （1）命令行交互

- 1、请在键盘上进行操作：持续按着Windows键不动，并且在这之后按下R

> 小提示：Windows键长这样![win](.\img\win.png)
>
> 以后，我们把这种几乎同时按下的操作做以下约定，比如上面的为『windows+R』

观察到效果如下，在电脑屏幕左下角有下列“窗口”弹出：

![00.README_学习准备_01](.\img\00.README_学习准备_01.png)

- 2、往“窗口”中输入『`cmd`』

  > 小提示：
  >
  > 快捷键『windows+R』打开的，其实此时是不需要用鼠标去点击那个窗口再输入的
  >
  > 你现在直接用键盘输出是会直接输入到里面的:smile:

  

- 3、点击“确定”或者按下键盘上的『enter』键

  ![00.README_学习准备_01](.\img\00.README_学习准备_02.png)

  观察到窗口消失，弹出类似下面的窗口:

  ![00.README_学习准备_01](.\img\00.README_学习准备_03.png)

  - 4、接着，我们在这个“窗口”中输入以下命令语句，然后按下『enter』键

  ```bat
echo Welcome
  ```
  
  观察到如下现象，命令行将你希望打印的“Welcome”输出来了:smile:

  ![00.README_学习准备_04](.\img\00.README_学习准备_04.png)

- 5、至此，你已经观察到了我们将要学习的命令行，输出`Welcome`的第一种方式，接下来让我们观察第2种方式。





### （2）编写批处理脚本

- 1、在你的桌面上新建一个叫`demo.txt`的文件![show](.\img\show.png)

> 注意：
>
> 此时，有的读者新建的文件，可能没有后缀名，请开启！
>
> 开启方法，请跳转本文第2节《**文件扩展名问题解决方案**》学习



- 2、在其中输出下面两行命令，保存

```bat
echo Welcome
pause
```

- 3、将原先的`.txt`文件后缀改为`.bat`或者`.cmd`，我们选择`.bat`

![show01](.\img\show01.png)



- 4、双击`demo.bat`尝试执行，观察现象如下

![show01](.\img\show02.png)

![00.README_学习准备_05](\img\00.README_学习准备_05.png)

- 5、至此你已经学会了另一种方式，输出`welcome`:smile:，那么这2种方式有什么区别和联系呢？

  稍安勿躁，等会你可以跟着“Windows历史的年轮”前去了解，接下来请耐心训练和观察一下本节的《配套训练》





## 二、文件扩展名问题解决方案



>本部分是用来解决部分“非计算机”方向读者的“扩展名”问题的



- 1、请按快捷键『windows+E』，然后在点击图中的“查看”![00.README_学习准备_06](.\img\00.README_学习准备_06.png)



- 2、然后，勾选“**文件扩展名**”，效果如下，然后你新建的文件就能看到“拓展名”了

  ![00.README_学习准备_06](.\img\00.README_学习准备_07.png)

- 3、至此问题就解决了:smile:





## 三、配套训练



- 1、请用“命令行交互”和“批处理脚本”两种方式进行训练
- 2、运行下列命令同时，请观察现象
- 3、如何可以的话，可以记忆这些简单命令，就是些简单的英语单词，相信你一定可以做到的:smile:
- 4、黑框框闹鬼:stuck_out_tongue_closed_eyes::stuck_out_tongue_closed_eyes::stuck_out_tongue_closed_eyes:提示：请在用“批处理脚本”编写的时候，记得在每个文件后，一定要加上`pause`这个单词，否则你会观察到”黑框框“一闪而过的效果，那可不是闹鬼:stuck_out_tongue_closed_eyes::stuck_out_tongue_closed_eyes::stuck_out_tongue_closed_eyes:
- 5、为节省文章篇幅，以下演示，均是笔者用“命令行交互”的方式测试的效果，你可以不能偷懒:smiling_imp:



### （1）第1组、时间类

#### 1、date

显示日期，某年某月某日，星期几，如果加上`/t`参数则只显示日期，而不用输入新日期。

```bat
C:\Users\MaxWell>date /T
12/17/2020 Thu

C:\Users\MaxWell>date
The current date is: 12/17/2020 Thu
Enter the new date: (mm-dd-yy)

```

> 解释：第2个语句，请按下『enter』，可不能随便输入数字，不然不小心把你电脑日期改了就不好
>
> 语句1和语句2都是：告知是2020年12月17日，星期四



#### 2、time

显示时间，几点几分
如果加上“/t”参数则只显示时间，而不用输入新时间

```bat

C:\Users\MaxWell>time /t
10:32 AM

C:\Users\MaxWell>time
The current time is: 10:32:02.48
Enter the new time:
```

> 解释：第2个语句，请按下『enter』，可不能随便输入数字，不然不小心把你电脑时间改了就不好了
>
> 语句1和语句2都是：告知是10点32分















### （2）第2组、一些零碎命令



#### 1、ver(version)

显示当前Windows操作系统的版本号

```bat
Microsoft Windows [Version 10.0.16299.1127]
(c) 2017 Microsoft Corporation。保留所有权利。

C:\Users\MaxWell>ver

Microsoft Windows [Version 10.0.16299.1127]
```



> 解释：上面告诉我们，笔者的电脑的版本是`Microsoft Windows [Version 10.0.16299.1127]`
>
> Tips:那么什么是电脑操作系统的版本呢？你又需要跟着第2节“Windows历史的年轮”前去了解:stuck_out_tongue_closed_eyes:，接下来请耐心训练和观察



#### 2、pause 

pause命令就是暂停的意思,防止批处理执行完后直接退出!    

运行 Pause 命令时，将显示下面的消息：  
`Press any key to continue. . .(或：请按任意键继续. . .)`

```bat
C:\Users\MaxWell>pause
Press any key to continue . . .
```



> 解释：
>
> 至此，你或者对于用“批处理脚本”编写的时候，在每个文件后，一定要加上`pause`这个单词有那么一点点感性的认识，但是还是不知道，为什么不加就会“黑框框”闪过？
>
> 原因：
>
> “Windows命令行交互方式“，本身**默认**就是执行完命令之后不会退出命令行
>
> “批处理脚本”方式，**默认**执行完后会退出命令行，这是**系统设计使然**，我们只好遵守:mask::mask::mask:




#### 3、exit

退出cmd命令行模式

```bat
exit
```



> 碎碎恋：
>
> 某些读者可能会用快捷键『Alt+F4』来关掉命令行（cmd）窗口
>
> 但在`PowerShell`中不能这么关闭，**只能**用exit！（powershell是什么？这个也在第2节“Windows历史的年轮”可以了解到:stuck_out_tongue_closed_eyes:，请耐心训练和观察最后一个，也是以后学习中最常用的一个命令，这买卖可不亏:smile:



#### 4、/?（最常用命令）

`/?`是求助命令

当你不记得某个命令的使用方式的时候，你就可以用这个方式，向你的电脑求助。

哪里不会，问哪里。



问`exit`命令是干啥的，使用的语法是怎样的，测试如下

```bat
C:\Users\MaxWell>exit /?
Quits the CMD.EXE program (command interpreter) or the current batch
script.

EXIT [/B] [exitCode]

  /B          specifies to exit the current batch script instead of
              CMD.EXE.  If executed from outside a batch script, it
              will quit CMD.EXE

  exitCode    specifies a numeric number.  if /B is specified, sets
              ERRORLEVEL that number.  If quitting CMD.EXE, sets the process
              exit code with that number.
```



> 解释：
>
> 很显然exit命令，除了用于我们先前那样退出之外，还有更加高级的用法，目前读者不用关心
>
> 恭喜你完成本节内容，请前往第2节《Windows历史的年轮》:yum::yum::yum:







## 四、高阶读者加餐

- 高阶读者，必然对计算机基础知识有所了解，我就只列出一些命令，请自行测试

`help`命令在老一些版本的Dos操作系统和Windows系统中，也是求助的命令。

