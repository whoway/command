# 第2讲-Part01.CMD界面美化



> 命令行启航—创造自己喜爱的界面
>
> 如何你想要界面不是，黑底白字，可以学习一下下面的命令进行美化:smile:





## （1）title

设置cmd命令行模式的**标题栏**信息

```bat
title 标题
```

测试效果：

![原始](.\img\01.old.png)

![新](.\img\02.new.png)



## （2）mode

调整命令提示符窗口大小，lines代表行数，cols代表列数

```bat
mode con lines=行数 cols=列数
```

测试现象：

![03.mode_old](.\img\03.mode_old.png)

![04.mode_cmd](.\img\04.mode_cmd.png)

![05.mode_new](.\img\05.mode_new.png)

Tips:如果设置得太小了，比如3行5列，就会报下面的错误

```bat
The screen cannot be set to the number of lines and columns specified.
//翻译：无法将屏幕设置为指定的行数和列数。
```



## （3）color(Colour)


注意:颜色属性由两个十六进制数字指定.第一个为背景,第二个为前景。

```txt
字符信息含义:
0(黑色)  1(蓝色)  2(绿色)  3(湖蓝色)  4(红色)  5(紫色)  6(黄色)  7(白色) 8(灰色)  9(淡蓝色)  
A(淡绿色)  B(淡浅绿色)  C(淡红色)  D(淡紫色) E(淡黄色) F(亮白色)
```


Color  

将颜色还原到cmd命令行模式启动时的颜色  

Color f 或Color 0f   

 将背景色设置为黑色,前景色设置为亮白色

> 注意: 设置好自己喜欢的颜色后,需要手动保存设置,否则在关闭cmd窗口后,下次启动时仍然为未设
> 置时的状态







