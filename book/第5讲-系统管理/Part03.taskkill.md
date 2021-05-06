# taskkill

语法
taskkill [/s Computer] [/u Domain\User [/p Password]]] [/fi FilterName] [/pid ProcessID]|[/im ImageName] [/f][/t]
参数

/s Computer
    指定远程计算机名称或 IP 地址（不能使用反斜杠）。默认值是本地计算机。 
/u Domain\User
    运行具有由 User 或 Domain\User 指定用户的帐户权限命令。默认值是当前登录发布命令的计算机的用户权限。 
/p Password
    指定用户帐户的密码，该用户帐户在 /u 参数中指定。 
/fi FilterName
    指定将要终止或不终止的过程的类型。以下是有效的筛选器名称、运算符和值：
    名称 	运算符 	值
    Hostname 	eq, ne 	任何有效字符串。
    状态 	eq, ne 	RUNNING|NOT RESPONDING
    Imagename 	eq, ne 	任何有效字符串。
    PID 	eg, ne, gt, lt, ge, le 	任何有效的正整数。
    Session 	eg, ne, gt, lt, ge, le 	任何有效的会话数。
    CPUTime 	eq, ne, gt, lt, ge, le 	hh:mm:ss 格式的有效时间。
mm 参数和 ss 参数应在 0 到 59 之间，hh 参数可以是任何一个有效的无符号的数值。
    Memusage 	eg, ne, gt, lt, ge, le 	任何有效的整数。
    用户名 	eq, ne 	任何有效的用户名 ([Domain\]User)。
    服务 	eq, ne 	任何有效字符串。
    Windowtitle 	eq, ne 	任何有效字符串。
/pid ProcessID
    指定将终止的过程的过程 ID。 
/im ImageName
    指定将终止的过程的图像名称。使用通配符 (*) 指定所有图像名称。 
/f
    指定将强制终止的过程。对于远程过程可忽略此参数，所有远程过程都将被强制终止。 
/t
    指定终止与父进程一起的所有子进程，常被认为是“树终止”。 
/?
    在命令提示符显示帮助。 

注释

    * 只有与筛选器一起指定时，通配符 (*) 才能被接受。
    * 无论是否指定 /f 参数，都会始终强制执行对远程过程的终止操作。
    * 向 HOSTNAME 筛选器提供计算机名将导致关机和中止所有过程。
    * 使用 tasklist 确定要终止的过程的过程 ID (PID)。
    * Taskkill 替代了 Kill 工具。

结束一个或多个任务或进程。可以根据进程 ID 或图像名来结束进程
例：taskkill /f /im notepad.exe
    taskkill /pid 1230 /pid 1241 /pid 1253
范例

下面的范例说明如何使用 taskkill 命令：

taskkill /pid 1230 /pid 1241 /pid 1253
taskkill /f /fi "USERNAME eq NT AUTHORITY\SYSTEM" /im notepad.exe
taskkill /s srvmain /f /im notepad.exe
taskkill /s srvmain /u maindom\hiropln /p p@ssW23 /fi "IMAGENAME eq note*" /im *
taskkill /s srvmain /u maindom\hiropln /fi "USERNAME ne NT*" /im *
taskkill /f /fi "PID ge 1000" /im *

