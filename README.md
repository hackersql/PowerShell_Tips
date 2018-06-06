# PowerShell_Tips

1.使用管道|来一次性完成你的工作，不要使用单行命令逐步执行。。。

2.使用Get-Help来获取你想要的命令，不要试图去记住这么多的命令，你只要知道该如何使用帮助命令就OK了。

3.Unblock-File解锁权限

4.$_保存当前上下文处理的元素。

5.Ctrl+J一个神奇的组合键，可以为我们创造程序示例代码，各个函数块等。

6.为脚本添加参数，然后只要输入脚本名 -Tab键就可以切换参数。

7.Get-Help 脚本名，可查看脚本自带参数

8.param(
    $a='如果有多个变量，后面加逗号',
    $b="创建参数"
)

8.(Get-Command Get-Random).Definition可查看定义

9.Get-Verb获取动词

10.Show-Command

11.Get-Help

12.pushd:记录当前位置

13.popd:返回到pushd的位置

14.Format-Table格式化显示

15.$var变量以$符号开头

16.${c:ip.txt}这会显示c盘下ip.txt中的内容

17.(Get-)+Tab循环显示可能的命令，shift+tab后退显示上个命令。

18.(Get-Service -)Tab循环显示可能的命令参数

19.(Get-Service )Tab循环显示可能的命令参数（实参）

20.Get-Help -Examples例子代码

21.Get-Help -Online在线查询

22.Get-Help -ShowWindow

23.Get-Help *log* 查找包含log的命令

24Get-Service | ConvertTo-Html -Property name,status | Out-File E:\service.html


25.转换格式
ConvertTo-Csv
ConvertTo-Html -Property只有html有这个参数，可以选择只打印某一列
ConvertTo-Json
ConvertTo-Xml
ConvertTo-SecureString

26.导出格式
```
Out-Default
Out-Host
Out-Null
Out-File文本
Out-GridView这个可以过滤查看
Out-Printer打印机
Out-String
```

27.-WhatIf在不确定操作会发生什么时使用
```
PS C:\> Get-Service *bi* |Stop-Service -WhatIf
What if: Performing the operation "Stop-Service" on target "Background Intelligent Transfer Service (BITS)".
What if: Performing the operation "Stop-Service" on target "Windows Biometric Service (WbioSrvc)".
```

28.-Confirm在执行不确定操作时会让你逐步确认操作
```
PS C:\> Get-Service *bi* |Stop-Service -Confirm

Confirm
Are you sure you want to perform this action?
Performing the operation "Stop-Service" on target "Background Intelligent Transfer
Service (BITS)".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): n

Confirm
Are you sure you want to perform this action?
Performing the operation "Stop-Service" on target "Windows Biometric Service (WbioSrvc)".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): n
```

29.|Select -Property 属性名，寻找自己需要的属性属性

30.Get-Process | Get-Member获取Get-Process的方法属性

31.Get-Process | Select-Object或者简写Select后面跟要显示的属性，按Tab键可来回查看属性。

32.Get-Process |select -Property ProcessName,CPU|sort cpu -Descending查看进程的名字和CPU，并以cpu来排序，默认是升序，参数-Descendin是降序。

33.$x = [xml](cat .\queries.xml)打开一个xml文件赋给变量x

34.$x.root.dbms[0].banner可查询xml文件中的指定节点

35.group分组

36.sort排序

37.where用作提取满足我们指定条件的内容

38.带｛$_.｝的where为功能丰富版
Get-Process | Where-Object {$_.ProcessName -eq "wechat"}
$_代表当前对象中的内容赋给_,在做比较时，如果是字符串加引号（单双引号都可以）
```
Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
-------  ------    -----      -----     ------     --  -- 
1063      83    80196     152356     166.30   2760   1 WeChat
```
简化版where不带｛$_.｝
```
PS E:\> Get-Process | where -Property ProcessName -eq "wechat"

Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
-------  ------    -----      -----     ------     --  -- -----------
   1055      83    80140     152328     166.86   2760   1 WeChat
```

39.显示模块路径
PS C:\> $env:PSModulePath -split ";"
C:\Users\Administrator\Documents\WindowsPowerShell
C:\Program Files\WindowsPowerShell\Modules
C:\Windows\system32\WindowsPowerShell\v1.0\Modules
