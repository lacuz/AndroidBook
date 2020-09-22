# ADB


|---|---|
|查看日志			 	|adb logcat|
|查看日志保存到指定文件	|adb logcat > D:/log.txt|
|查看日志，过滤指定内容	|adb shell “logcat &#124;  grep com.lanyou.jvstapp” >D:/log.txt|
|查看日志，过滤指定内容	|adb shell “logcat &#124;  grep com.lanyou.jvstapp  &#124; tee D:/log.txt”|
|输出标签为TAG的log级别大于X的信息 | adb logcat Test:I |

adb reverse tcp:8081 tcp:8081 释放端口


adb shell uiautomator dump /sdcard/ui.xml 获取手机屏幕布局信息




## pm命令
adb shell pm list packages [options] \<FILTER>

|---|---|
|获取所有应用信息|adb shell pm list packages |
|输出包和包相关联的文件|adb shell pm list packages **-f**|
|只输出禁用的包|adb shell pm list packages **-d**|
|只输出启用的包|adb shell pm list packages **-e**|
|只输出系统的包|adb shell pm list packages **-s**|
|只输出第三方的包|adb shell pm list packages **-3**|
|只输出包和安装信息（安装来源）|adb shell pm list packages **-i**|
|只输出包和未安装包信息（安装来源）|adb shell pm list packages **-u**|
|根据用户id查询用户的空间的所有包，<br>USER_ID代表当前连接设备的顺序，从零开始|adb shell pm list packages --user \<USER_ID>|

adb shell pm uninstall -k --user 0 packageName -k表示保存数据


示例：
列出所有包含小米的包
adb shell pm list packages "xiaomi"



## dumps命令
查看当前设备所运行的包名 ，activity名

adb shell dumpsys window w | findstr name | findstr \/


## getprop
获取系统版本
adb shell getprop ro.build.version.sdk