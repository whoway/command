#### （4）tasklist

Tasklist命令用来显示运行在本地或远程计算机上的所有进程，带有多个执行参数。
使用格式
　　Tasklist [/S system [/U username [/P [password]]]] [/M [module] | /SVC | /V] [/FI filter] [/FO format] [/NH]
参数含义
　　/S system　指定连接到的远程系统。
　　/U [domain\]user　指定使用哪个用户执行这个命令。
　　/P [password]　为指定的用户指定密码。
　　/M [module]　列出调用指定的DLL模块的所有进程。如果没有指定模块名，显示每个进程加载的所有模块。
　　/SVC　显示每个进程中的服务。当 /fo 参数设置为 TABLE 时有效
　　/V　显示详细信息。
　　/FI filter　显示一系列符合筛选器指定的进程。
　　/FO format　指定输出格式，有效值：TABLE、LIST、CSV。
　　/NH　指定输出中不显示栏目标题。只对TABLE和CSV格式有效。