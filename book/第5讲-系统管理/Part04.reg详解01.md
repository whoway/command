
# 系统管理


| 命令     | 用途                                        |
| -------- | ------------------------------------------- |
| at       | 安排在特定日期和时间运行命令和程序          |
| shutdown | 立即或定时关机或重启                        |
| taskkill | 结束进程(WinXPHome版中无该命令)             |
| tasklist | 显示进程列表(Windows XP Home Edition中没有) |
| reg      | 注册表控制台工具                            |







# reg



在写一些批处理文件的时候，我们经常要对系统的注册表进行相关的操作。图形界面

下可以通过在CMD命令行模式下直接输入regedit进行操作。如果是在其他的场合，并

且没有图形界面的情况下我们就可以通过reg这个命令来对系统的注册表或者是远程的

注册表进行增删的操作了。

reg命令主要用来对注册表子项信息和注册表项值中的值执行添加、更改、导入、导出

以及其他操作。建议大家在修改注册表之前先对其进行备份。以免一些不必要的麻烦。

考虑到reg命令的参数过多，大家只需要记一些比较重要和常用的参数就可以了。

Windows 控制台注册表工具 - 版权所有 (C) Microsoft Corp. 1981-2001.  保留所有权繰EG Operation [参数列表]

  Operation  [ QUERY   | ADD    | DELETE  | COPY    |
               SAVE    | LOAD   | UNLOAD  | RESTORE |
               COMPARE | EXPORT | IMPORT ]
返回代码: (除了 REG COMPARE)
  0 - 成功
  1 - 失败

要得到有关某个操作的帮助，请键入:

  REG Operation /?

例如:

  REG QUERY /?
  REG ADD /?
  REG DELETE /?
  REG COPY /?
  REG SAVE /?
  REG RESTORE /?
  REG LOAD /?
  REG UNLOAD /?
  REG COMPARE /?

### 1、Reg Add		//掌握

用该命令加入一个新的指定键值。

REG ADD KeyName [/v ValueName | /ve] [/t Type] [/s Separator] [/d Data] [/f]

  KeyName  [\\Machine\]FullKey

           远程机器的机器名 - 忽略则默认到当前机器。 远程机器上只有 HKLM 和 HKU。
    
           FullKey  ROOTKEY\SubKey
    
           ROOTKEY  [ HKLM | HKCU | HKCR | HKU | HKCC ]
    
           SubKey   所选 ROOTKEY 下注册表项的完整名

  /v       所选项之下要添加的值名     (v-value-值)

  /ve      为注册表项添加空白值名<无名称>

  /t       RegKey 数据类型     (t-type-类型)

           [ REG_SZ    | REG_MULTI_SZ  | REG_DWORD_BIG_ENDIAN    |
    
             REG_DWORD | REG_BINARY    | REG_DWORD_LITTLE_ENDIAN |
    
             REG_NONE  | REG_EXPAND_SZ ] 如果忽略，则采用 REG_SZ

  /s       指定一个在 REG_MULTI_SZ 数据字符串中用作分隔符的字符，如果忽略，则将 "\0" 用作分隔符  (Separator-分隔符)

  /d       分配给添加的注册表 ValueName 的数据   (d-data-数据)

  /f       不用提示就强行改写现有注册表项        (f-force-强制)

例如:

  REG ADD \\ABC\HKLM\Software\MyCo

    添加远程机器 ABC 上的一个注册表项 HKLM\Software\MyCo


  REG ADD HKLM\Software\MyCo /v Data /t REG_BINARY /d fe340ead

    添加一个值(名称: Data，类型: REG_BINARY，数据: fe340ead)


  REG ADD HKLM\Software\MyCo /v MRU /t REG_MULTI_SZ /d fax\0mail

    添加一个值(名称: MRU，类型: REG_MUTLI_SZ，数据: fax\0mail\0\0)


  REG ADD HKLM\Software\MyCo /v Path /t REG_EXPAND_SZ /d %%systemroot%%

    添加一个值(名称: Path，类型: REG_EXPAND_SZ，数据: %systemroot%)
    
    注意:  在扩充字符串中使用双百分比符号( %% )

### 2、Reg Compare		//了解 

将当前(本地计算机)的注册表与另外一个注册表或另外一个远程计算机上的注册表进行比较。将比较输出到一个文件上。

REG COMPARE KeyName1 KeyName2 [/v ValueName | /ve] [Output] [/s]

  KeyName    [\\Machine\]FullKey

    Machine  远程机器名 - 省略当前机器的默认值
    
    FullKey  ROOTKEY\SubKey
    
             如果没有指定 FullKey2，FullKey2 则跟 FullKey1 相同
    
    ROOTKEY  [ HKLM | HKCU | HKCR | HKU | HKCC ]
    
    SubKey   所选 ROOTKEY 下的注册表项的全名

  ValueName  所选注册表项下的要比较的值的名称

             省略时，该项下的所有值都会得到比较

  /ve        比较空白值<no name>名称的值

  /s         比较所有子项和值

  Output     [/oa | /od | /os | /on]

             省略时，只显示不同的结果
    
    /oa      显示所有不同和匹配结果
    
    /od      只显示不同的结果
    
    /os      只显示匹配结果
    
    /on      不显示结果

返回代码:

  0 - 成功，比较的结果相同

  1 - 失败

  2 - 成功，比较的结果不同

例如:

  REG COMPARE HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp

    将注册表项 MyApp 下的所有值跟 SaveMyApp 比较


  REG COMPARE HKLM\Software\MyCo HKLM\Software\MyCo1 /v Version

    比较注册表项 MyCo 和 MyCo1 下的值 Version


  REG COMPARE \\ZODIAC\HKLM\Software\MyCo \\. /s

    将 ZODIAC 上 HKLM\Software\MyCo 下的所有子项和值和当前机器上的相同项比较

### 3、Reg Copy		//掌握

将当前的注册表或远程计算机上的注册表拷贝到一个新的位置(或计算机上)。

REG COPY KeyName1 KeyName2 [/s] [/f]

  KeyName    [\\Machine\]FullKey

    Machine  远程机器名 - 忽略当前机器的默认值
    
    FullKey  ROOTKEY\SubKey
    
    ROOTKEY  [ HKLM | HKCU | HKCR | HKU | HKCC ]
    
    SubKey   所选 ROOTKEY 下的注册表项的全名

  /s         复制所有子项和值

  /f         不用提示就强行复制

例如:

  REG COPY HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp /s

    将注册表项 MyApp 下的所有子项和值复制到注册表项 SaveMyApp


  REG COPY \\ZODIAC\HKLM\Software\MyCo HKLM\Software\MyCo1

    将 ZODIAC 上注册表项 MyCo 下的所有值复制到当前机器上的注册表项 MyCo1

### 4、Reg Delete		//掌握

删除一个注册表、注册表键值或子键值。

REG DELETE KeyName [/v ValueName | /ve | /va] [/f]

  KeyName    [\\Machine\]FullKey

    Machine  远程机器名 - 忽略当前机器的默认值
    
    FullKey  ROOTKEY\SubKey
    
    ROOTKEY  [ HKLM | HKCU | HKCR | HKU | HKCC ]
    
    SubKey   所选 ROOTKEY 下的注册表项的全名

  ValueName  所选项下的要删除的值的名称省略时，该项下的所有子项和值都会被删除

  /ve        删除空白值名称<no name>的值

  /va        删除该项下的所有值

  /f         不用提示就强行删除

例如:

  REG DELETE HKLM\Software\MyCo\MyApp\Timeout

    删除注册表项 Timeout 及其所有子项和值


  REG DELETE \\ZODIAC\HKLM\Software\MyCo /v MTU

    删除 ZODIAC 上 MyCo 下的注册表项 MTU

### 5、Reg Export		//掌握

将注册表导出到一个文件上，仅适用于在本地计算机导出。

REG EXPORT KeyName FileName

  Keyname    ROOTKEY\SubKey (local machine only)

    ROOTKEY  [ HKLM | HKCU | HKCR | HKU | HKCC ]
    
    SubKey   所选 ROOTKEY 下的注册表项的全名

  FileName   要导出的磁盘文件名

例如:

  REG EXPORT HKLM\Software\MyCo\MyApp AppBkUp.reg

    将注册表项 MyApp 的所有子项和值导出到文件 AppBkUp.reg

### 6、Reg Import--(掌握)

将(备份的)一个注册表文件导入到计算机中，仅适用于在本地计算机。

REG IMPORT FileName

  FileName  要导入的磁盘文件名(只用于本地机器)

例如:

  REG IMPORT AppBkUp.reg

    从文件 AppBkUp.reg 导入注册表项

### 7、Reg Load		//了解

从备份的注册表中临时装入一个指定的键值，这种操作类似于使用注册表编辑器导入某一个键值。

REG LOAD KeyName FileName

  KeyName    ROOTKEY\SubKey (只是本地机器的)

    ROOTKEY  [ HKLM | HKU ]
    
    SubKey   要将配置单元文件加载进的注册表项名称。创建一个新的注册表项

  FileName   要加载的配置单元文件名，您必须使用 REG SAVE 来创建这个文件

例如:

  REG LOAD HKLM\TempHive TempHive.hiv

    将文件 TempHive.hiv 加载到注册表项 HKLM\TempHive

### 8、Reg Query		//掌握

显示相关项目的信息，此处所指项目可以是整个注册表之中的根键、子键或其集合。

REG QUERY KeyName [/v ValueName | /ve] [/s]

  KeyName    [\Machine\]FullKey

    Machine  远程机器名 - 忽略当前机器的默认值
    
    FullKey  格式为 ROOTKEY\SubKey
    
         ROOTKEY  [ HKLM | HKCU | HKCR | HKU | HKCC ]
    
         SubKey   所选 ROOTKEY 下的注册表项的全名

  /v  查询特定注册表项

         ValueName  所选项下的要查询的值的名称省略时，该项下的所有值都会得到查询

  /ve        查询默认值或空白值名称<no name>

  /s         查询所有子项和值

例如:

  REG QUERY HKLM\Software\Microsoft\ResKit /v Version

    显示注册表值 Version 的值


  REG QUERY HKLM\Software\Microsoft\ResKit\rt\Setup /s

    显示注册表项 Setup 下的所有子项和值

### 9、Reg Restore 恢复注册表		//了解

REG RESTORE KeyName FileName

  KeyName    ROOTKEY\SubKey (只是本地机器)

    ROOTKEY  [ HKLM | HKCU | HKCR | HKU | HKCC ]
    
    SubKey   要将配置单元文件还原到的注册表项全名。改写现有项的值和子项

  FileName   要还原的配置单元文件名

             您必须使用 REG SAVE 来创建这个文件

例如:

  REG RESTORE HKLM\Software\Microsoft\ResKit NTRKBkUp.hiv

    还原文件 NTRKBkUp.hiv，改写注册表项 ResKit

10、Reg Save		//了解

保存注册表，这个操作是类似注册表编辑器中的将整个注册表导出到一个文件中，当然，也可以导出某个键或其下面的子键的集合。

REG SAVE KeyName FileName

  KeyName    ROOTKEY\SubKey

    ROOTKEY  [ HKLM | HKCU | HKCR | HKU | HKCC ]
    
    SubKey   所选 ROOTKEY 下的注册表项的全名

  FileName   要保存的磁盘文件名。如果没有指定路径，文件会在调用进程的当前文件夹中得到创建

例如:

  REG SAVE HKLM\Software\MyCo\MyApp AppBkUp.hiv

    将配置单元 MyApp 保存到当前文件夹中的文件 AppBkUp.hiv

## 11、Reg Unload		//了解

移去装入的部分，移去原来用Reg load命令装入的部分键或其以下的子键集合。

REG UNLOAD KeyName

  KeyName    ROOTKEY\SubKey (只是本地机器的)

    ROOTKEY  [ HKLM | HKU ]
    
    SubKey   要卸载的配置单元的注册表项名称

例如:

  REG UNLOAD HKLM\TempHive

    卸载 HKLM 中的配置单元 TempHive




Reg概述：
    对注册表子项信息和注册表项值中的值执行添加、更改、导入、导出以及其他操作。


    Reg 命令包括：
    Reg Add / Reg Compare / Reg Copy / Reg Delete / Reg Export / Reg Import / Reg Load / Reg Query / Reg Restore / Reg Save / Reg Unload
    
    Reg Add
    将新的子项或项添加到注册表中。
    
    语法：
    Reg Add KeyName [{/v ValueName | /ve}] [/t DataType] [/s Separator] [/d Data] [/f]
    
    参数：
    KeyName 指定要添加的子项或项的完整路径。要指定远程计算机，
请包括计算机名（以 \\ComputerName\ 格式表示），并将其作为 KeyName 的一部分。
省略 \\ComputerName\ 会导致默认对本地计算机的操作。KeyName 必须包括一个有效的根键。
有效根键包括 HKLM、HKCU、HKCR、HKU 以及HKCC。如果指定了远程计算机，则有效根键是 HKLM 和 HKU。

```bat
/v ValueName
指定要添加到指定子项下的注册表项名称。

/ve
指定添加到注册表中的注册表项为空值。

/t Type
指定注册表项的类型。Type 必须是以下几种类型之一：
Reg_SZ
Reg_MULTI_SZ
Reg_DWORD_BIG_ENDIAN
Reg_DWORD
Reg_BINARY
Reg_DWORD_LITTLE_ENDIAN
Reg_LINK
Reg_FULL_RESOURCE_DESCRIPTOR
Reg_EXPAND_SZ

/s Separator
当指定了 Reg_MULTI_SZ 数据类型并且需要列出多个项时，指定用来分隔数据的多个实例的字符。如果没有指定，将使用默认分隔符“\0”。 

/d Data
指定新注册表项的数据。

/f
添加注册表项而不要求确认。

/?
在命令提示符处显示 Reg Add 的帮助。

注释：
? 该操作不能添加子树。该版本的 Reg 在添加子项时无需请求确认。
? 下表列出了 Reg Add 操作的返回值。
值 描述
0   成功
1   失败
? 对于 Reg_EXPAND_SZ 项类型，在 /d 参数内将插入符号 ( ^ ) 与“%”一起使用。

示例：
要在远程计算机 ABC 上添加 HKLM\Software\MyCo 项，请键入：
Reg ADD \\ABC\HKLM\Software\MyCo

要将一个注册表项添加到 HKLM\Software\MyCo，选项为值名：Data；类型：Reg_BINARY；数值数据：fe340ead；请键入：
Reg ADD HKLM\Software\MyCo /v Data /t Reg_BINARY /d fe340ead

要将一个多值注册表项添加到 HKLM\Software\MyCo，选项为值名：MRU；数据类型：Reg_MULTI_SZ；数值数据：fax\0mail\0\0；请键入：
Reg ADD HKLM\Software\MyCo /v MRU /t Reg_MULTI_SZ /d fax\0mail\0\0

要将一个扩展的注册表项添加到 HKLM\Software\MyCo，选项为值名：Path；数据类型：Reg_EXPAND_SZ；数值数据：%systemroot%；请键入：
Reg ADD HKLM\Software\MyCo /v Path /t Reg_EXPAND_SZ /d ^%systemroot^%

Reg Compare
比较指定的注册表子项或项。

语法：
Reg Compare KeyName1 KeyName2 [{/v ValueName | /ve}] [{/oa | /od | /os | on}] [/s]

参数：
KeyName1
指定要比较的第一个子项的完整路径。要指定远程计算机，请包括计算机名（以\\ComputerName\ 格式表示），并将其作为 KeyName 的一部分。省略 \\ComputerName\ 会导致默认对本地计算机的操作。KeyName 必须包括一个有效的根键。有效根键包括 HKLM、HKCU、HKCR、HKU 以及 HKCC。如果指定了远程计算机，则有效根键是 HKLM 和 HKU。

KeyName2
指定要比较的第二个子项的完整路径。要指定远程计算机，请包括计算机名（以 \\ComputerName\ 格式表示），并将其作为 KeyName 的一部分。省略 \\ComputerName\ 会导致默认对本地计算机的操作。只在 KeyName2 中指定计算机名会导致该操作使用到 KeyName1 中指定的子项的路径。KeyName 必须包括一个有效的根键。有效根键包括 HKLM、HKCU、HKCR、HKU 以及 HKCC。如果指定了远程计算机，则有效根键是HKLM和HKU。

/v ValueName
指定要比较的子项下的值名称。

/ve
指定只比较值名称为 null 的项。

[{/oa | /od | /os | on}]
指定如何显示比较操作的结果。默认设置是 /od。下表列出了每一个选项。

值     描述
/oa   指定显示所有不同点和匹配点。默认情况下，仅列出不同点。
/od   指定仅显示不同点。这是默认操作。
/os   指定仅显示匹配点。默认情况下，仅列出不同点。
/on   指定不显示任何内容。默认情况下，仅列出不同点。

/s
递归地比较所有子项和项。

/?
在命令提示符处显示 Reg Compare 的帮助。

注释：
? 下表列出了 Reg Compare 操作的返回值。
值  描述
0    比较成功且结果相同。
1    比较失败。
2    比较成功并找到不同点。

? 下表列出了结果中显示的符号。
符号 描述
=       KeyName1 数据等于 KeyName2 数据
<       KeyName1 数据小于 KeyName2 数据
>       KeyName1 数据大于 KeyName2 数据

示例：
要将 MyApp 项下的所有值与 SaveMyApp 项下的所有值进行比较，请键入：
Reg COMPARE HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp

要比较 MyCo 项下的 Version 的值和 MyCo1 项下的 Version 的值，请键入：
Reg COMPARE HKLM\Software\MyCo HKLM\Software\MyCo1 /v Version

要将计算机 ZODIAC 上 HKLM\Software\MyCo 下的所有子项和值与当前计算机上 HKLM\Software\MyCo 下的所有子项和值进行比较，请键入： 
Reg COMPARE \\ZODIAC\HKLM\Software\MyCo \\. /s

Reg Copy
将一个注册表项复制到本地或远程计算机的指定位置。 

语法：
Reg Copy KeyName1 KeyName2 [/s] [/f] 

参数：
KeyName1 
指定要复制子项的完整路径。要指定远程计算机，请包括计算机名（以 \\ComputerName\ 格式表示），并将其作为 KeyName 的一部分。省略\\ComputerName\ 会导致默认对本地计算机的操作。KeyName 必须包括一个有效的根键。有效根键包括 HKLM、HKCU、HKCR、HKU 以及 HKCC。如果指定了远程计算机，则有效根键是 HKLM 和 HKU。 

KeyName2 

指定子项目的地的完整路径。要指定远程计算机，请包括计算机名（以 \\ComputerName\ 格式表示），并将其作为 KeyName 的一部分。省略 \\ComputerName\会导致默认对本地计算机的操作。KeyName 必须包括一个有效的根键。有效根键包括 HKLM、HKCU、HKCR、HKU 以及 HKCC。如果指定了远程计算机，则有效根键是 HKLM 和 HKU。 

/s
复制指定子项下的所有子项和项。 

/f 
不要求确认而直接复制子项。 

/?
在命令提示符处显示 Reg Copy 的帮助。 

注释  ：
? 在复制子项时 Reg 不请求确认。 
? 下表列出了 Reg Copy 操作的返回值。
值 描述
0   成功 
1   失败 

示例：

要将 MyApp 项下的所有子项和值复制到 SaveMyApp 项，请键入：
Reg COPY HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp /s 

要将计算机 ZODIAC 上的 MyCo 项下的所有值复制到当前计算机上的 MyCo1 项，请键入：
Reg COPY \\ZODIAC\HKLM\Software\MyCo HKLM\Software\MyCo1 

Reg Delete
从注册表删除子项或项。

语法：
Reg Delete KeyName [{/v ValueName | /ve | /va}] [/f]

参数：

KeyName
指定要删除的子项或项的完整路径。要指定远程计算机，请包括计算机名（以 \\ComputerName\ 格式表示），并将其作为 KeyName 的一部分。省略 \\ComputerName\ 会导致默认对本地计算机的操作。KeyName 必须包括一个有效的根键。有效根键包括 HKLM、HKCU、HKCR、HKU 以及 HKCC。如果指定了远程计算机，则有效根键是 HKLM 和 HKU。

/v ValueName
删除子项下的特定项。如果未指定项，则将删除子项下的所有项和子项。

/ve
指定只可以删除为空值的项。

/va
删除指定子项下的所有项。使用本参数不能删除指定子项下的子项。

/f
无需请求确认而删除现有的注册表子项或项。

/?
在命令提示符处显示 Reg Delete 的帮助。

注释：
? 下表列出了 Reg Delete 操作的返回值。 
值 描述 
0    成功
1    失败

示例：

要删除注册表项 Timeout 以及其所有子项和值，请键入：
Reg DELETE HKLM\Software\MyCo\MyApp\Timeout 

要删除计算机 ZODIAC 上 HKLM\Software\MyCo 下的注册表值 MTU，请键入：
Reg DELETE \\ZODIAC\HKLM\Software\MyCo /v MTU

Reg Export 
将本地计算机的指定子项、项和值复制到一个文件中，以便传输到其他服务器。 

语法：
Reg export KeyName FileName [/y]

参数：
KeyName 
指定子项的完全路径。Export 操作仅可在本地计算机上工作。KeyName 必须包括一个有效的根键。有效根键包括 HKLM、HKCU、HKCR、HKU 以及 HKCC。 

FileName
指定在操作期间创建的文件的名称和路径。该文件必须具有 .Reg 扩展名。 

/y
不要求确认即覆盖任何现有的名称为 FileName 的文件。 

/?
在命令提示符处显示 Reg Export 的帮助。 

注释： 
? 下表列出了 Reg Export 操作的返回值。
值 描述
0   成功 
1   失败 

示例： 
要将 MyApp 项的所有子项和值的内容导出到文件 AppBkUp.Reg，请键入：
Reg Export HKLM\Software\MyCo\MyApp AppBkUp.Reg

Reg Import 
将包含已导出的注册表子项、项和值的文件的内容复制到本地计算机的注册表中。

语法：
Reg Import FileName 

参数：
FileName 
指定其内容将复制到本地计算机注册表中的文件的名称和路径。此文件必须使用 Reg export 预先创建。 

/? 
在命令提示符处显示 Reg Import 的帮助。 

注释： 
? 下表列出了 Reg Import 操作的返回值。
值 描述
0   成功
1   失败 

示例： 
要从名为 AppBkUp.Reg 的文件导入注册表项，请键入：
Reg Import AppBkUp.Reg

Reg Load 
将保存的子项和项写回到注册表的不同子项中。与用于进行疑难解答或编辑注册表项的临时文件一起使用。 

语法：
Reg load KeyName FileName 

参数：
KeyName
指定要加载的子项的完整路径。要指定远程计算机，请包括计算机名（以 \\ComputerName\ 格式表示），并将其作为 KeyName 的一部分。省略 \\ComputerName\ 会导致默认对本地计算机的操作。KeyName 必须包括一个有效的根键。有效根键包括 HKLM、HKCU、HKCR、HKU 以及 HKCC。如果指定了远程计算机，则有效根键是 HKLM 和 HKU。 

FileName
指定要加载的文件的名称和路径。必须使用 .hiv 作为扩展名的 Reg Save 操作预先创建该文件。 

/? 
在命令提示符处显示 Reg Load 的帮助。 

注释：
? 下表列出了 Reg Load 操作的返回值。
值 描述
0   成功 
1   失败 

示例：
要将名为 TempHive.hiv 的文件加载到 HKLM\TempHive 项，请键入：
Reg LOAD HKLM\TempHive TempHive.hiv

Reg Quer
返回位于注册表中指定的子项下的下一层子项和项的列表。

语法：
Reg query KeyName [{/v ValueName | /ve}] [/s] [/se Separator] [/f Data] [{/k | /d}] [/c] [/e] [/t Type] [/z]

参数：
KeyName
指定子项的完全路径。要指定远程计算机，请包括计算机名（以 \\ComputerName\ 格式表示），并将其作为 KeyName 的一部分。省略 \\ComputerName\会导致默认对本地计算机的操作。KeyName 必须包括一个有效的根键。有效根键包括 HKLM、HKCU、HKCR、HKU 以及 HKCC。如果指定了远程计算机，则有效根键是 HKLM 和 HKU。

/v ValueName
指定要查询的注册表值名称。如果省略，则返回 KeyName 的所有值名称。如果还使用了 /f 选项，则此参数的 ValueName 是可选的。 

/ve
查询空白的值名称。

/s
指定该参数递归查询所有子项和值名称。

/se Separator
指定单值分隔符，以搜索 Reg_MULTI_SZ 类型的值名称。如果没有指定 Separator，则使用“\0”。

/f Data
指定要搜索的数据或模式。如果字符串包含空格，则使用双引号。如果未指定，则使用通配符 ("*") 作为搜索模式。

/k
指定只在项名称中搜索。

/d
指定只在数据中搜索。

/c
指定查询是区分大小写的。默认情况下，查询是不区分大小写的。

/e
指定只返回完全匹配项。默认情况下，返回所有匹配项。

/t Type
指定要搜索的注册表类型。有效的类型包括：Reg_SZ、Reg_MULTI_SZ、Reg_EXPAND_SZ、Reg_DWORD、Reg_BINARY、Reg_NONE。如果未指定，则搜索所有类型。

/z
指定在搜索结果中包括注册表类型的数字同等物。

/?
在命令提示符处显示 Reg Query 的帮助。

注释：
? 下表列出了 Reg Query 操作的返回值。
值 描述 
0   成功 
1   失败 

示例：
要显示 HKLM\Software\Microsoft\ResKit 项中的名称值 Version 的值，请键入：
Reg QUERY HKLM\Software\Microsoft\ResKit /v Version

要显示远程计算机 ABC 上的 HKLM\Software\Microsoft\ResKit\Nt\Setup 项下的所有子项和值，请键入：
Reg QUERY \\ABC\HKLM\Software\Microsoft\ResKit\Nt\Setup /s

要使用“#”作为分隔符显示 Reg_MULTI_SZ 类型的所有子项和值，请键入：
Reg QUERY HKLM\Software\Microsoft\ResKit\Nt\Setup /se #

要显示数据类型 Reg_SZ 的 HKLM 根下的“SYSTEM”的完全匹配并且区分大小写的匹配项的项、值和数据，请键入：
Reg QUERY HKLM /f SYSTEM /t Reg_SZ /c /e

要显示数据类型 Reg_BINARY 的根键 HKCU 下的数据中的“0F”的匹配项的项、值和数据，请键入：
Reg QUERY HKCU /f 0F /d /t Reg_BINARY

要显示 HKLM\SOFTWARE 下的值名称 null（默认值）的值和数据，请键入：
Reg QUERY HKLM\SOFTWARE /ve

Reg Restore
将保存的子项和项写回到注册表。 

语法：
Reg restore KeyName FileName

参数：
KeyName
指定要还原的子项的完整路径。Restore 操作仅在本地计算机上工作。KeyName 必须包括一个有效的根键。有效根键包括 HKLM、HKCU、HKCR、HKU 以及 HKCC。

FileName
指定其内容将写回到注册表中的文件的名称和路径。必须使用 .hiv 作为扩展名的 Reg save 操作预先创建该文件。

/?
在命令提示符处显示 Reg Restore 的帮助。

注释：
? 编辑任何注册表项之前，请使用 Reg Save 操作保存父子项。如果编辑失败，则可以使用 Reg Restore 操作还原原来的子项。 
? 下表列出了 Reg Restore 操作的返回值。 
值 描述
0   成功 
1   失败

示例：
要将名为 NTRKBkUp.hiv 的文件还原到 HKLM\Software\Microsoft\ResKit 项，并覆盖该项的现有内容，请键入：
Reg RESTORE HKLM\Software\Microsoft\ResKit NTRKBkUp.hiv

Reg Save
将指定的子项、项和注册表值的副本保存到指定文件中。 

语法：
Reg save KeyName FileName [/y]

参数：
KeyName
指定子项的完全路径。要指定远程计算机，请包括计算机名（以 \\ComputerName\ 格式表示），并将其作为 KeyName 的一部分。省略\\ComputerName\会导致默认对本地计算机的操作。KeyName 必须包括一个有效的根键。有效根键包括 HKLM、HKCU、HKCR、HKU 以及 HKCC。如果指定了远程计算机，则有效根键是 HKLM 和 HKU。

FileName
指定所创建的文件的名称和路径。如果未指定路径，则使用当前路径。

/y
不要求确认即覆盖任何现有的名称为 FileName 的文件。

/?
在命令提示符处显示 Reg Save 的帮助。

注释：
? 下表列出了 Reg Save 操作的返回值。
值 描述 
0   成功 
1   失败
? 编辑任何注册表项之前，请使用 Reg Save 操作保存父子项。如果编辑失败，则可以使用 Reg Restore 操作还原原来的子项。 

示例：
要将配置单元 MyApp 作为名为 AppBkUp.hiv 的文件保存到当前文件夹中，请键入：
Reg SAVE HKLM\Software\MyCo\MyApp AppBkUp.hiv

Reg Unload
使用 Reg Load 操作删除已加载的部分注册表。

语法：
Reg Unload KeyName

参数：

KeyName
指定要卸载的子项的完整路径。要指定远程计算机，请包括计算机名（以 \\ComputerName\格式表示），并将其作为 KeyName 的一部分。省略 \\ComputerName\ 会导致默认对本地计算机的操作。KeyName 必须包括一个有效的根键。有效根键包括 HKLM、HKCU、HKCR、HKU 以及 HKCC。如果指定了远程计算机，则有效根键是 HKLM 和 HKU。

/?
在命令提示符处显示 Reg Unload 的帮助。

注释：
? 下表列出了 Reg Unload 操作的返回值。
值 描述
0   成功
1   失败

示例：
要卸载 HKLM 中的配置单元 TempHive，请键入：
Reg UNLOAD HKLM\TempHive
```
