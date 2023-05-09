# ADB

window下shell后面尽量加双引号

adb reverse tcp:8081 tcp:8081 释放端口


adb shell uiautomator dump /sdcard/ui.xml 获取手机屏幕布局信息


## install 
adb install -r test.apk
adb install -r 保留数据和缓存文件，重新安装，升级,替换已存在的应用程序，也就是说强制安装
adb install -l 锁定该应用程序
adb install -t 允许测试包
adb install -s 把应用程序安装到sd卡上
adb install -d 允许进行将见状，也就是安装的比手机上带的版本低
adb install -g 为应用程序授予所有运行时的权限

## uninstall
卸载app但保留数据和缓存文件
adb uninstall -k cnblogs.apk


## pm命令
adb shell pm list packages [options] \<FILTER>

||指令|
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


## am
 adb shell am force-stop 包名
 adb shell am start -n 包名/Activity路径
 adb shell am start -a android.intent.action.VIEW -d http://testerhome.com 启动默认浏览器打开一个网页例
 adb shell am monitor        监控 crash 与 ANR
 adb shell am startservice    启动一个服务
 adb shell am broadcast       发送一个广播

## dumps
查看当前设备所运行的包名 ，activity名

adb shell dumpsys window w | findstr name | findstr \/

查看包名版本

adb shell pm dump 包名 | findstr version

## wm
查看分辨率：wm size
修改分辨率：wm size 1440x2560
还原初设置：wm size reset
查看密度：wm density
修改密度：wm density 480
还原设置：wm density reset

## getprop
获取系统api版本
adb shell getprop ro.build.version.sdk
获取系统版本
adb shell getprop ro.build.version.release
查看设备重启的原因
adb shell getprop sys.boot.reason
获取手机相关制造商信息
adb shell "getprop | grep -E model\|version.sdk\|manufacturer\|hardware\|platform\|revision\|serialno\|product.name\|brand"
获取手机系统信息（ CPU，厂商名称等）
adb shell "cat /system/build.prop | grep "product""
获取手机设备型号
adb shell getprop ro.product.model
获取手机的序列号
adb shell getprop ro.serialno
adb get-serialno
获取手机MAC地址
adb shell cat /sys/class/net/wlan0/address
获取手机内存信息
adb shell cat /proc/meminfo
获取手机存储信息
adb shell df
获取手机内部存储信息
adb shell df /data
获取Android设备屏幕分辨率
adb shell "dumpsys window | grep mUnrestrictedScreen"
查看目录下的文件大小
adb shell du -sh *
查看正在运行的Services
adb shell dumpsys activity services [<packagename>]
查看正在运行的Activity
adb shell dumpsys activity [<packagename>]

## 删除命令
adb shell 进入Android Linux命令中
rm  -r  /mnt/sdcard/a.mp3 
删除文件夹的时候需要加上-r参数 
cd dir 
rm *    删除dir中所有文件

## logcat
||指令|
|:---|:---|
|查看日志			 	|adb logcat|
|查看日志保存到指定文件	|adb logcat > D:/log.txt|
|查看日志，过滤指定内容	|adb shell “logcat -s *:E &#124;  grep com.lanyou.jvstapp” >D:/log.txt|
|查看日志，过滤指定内容	|adb shell “logcat &#124;  grep com.lanyou.jvstapp  &#124; tee D:/log.txt”|
|输出标签为TAG的log级别大于X的信息 | adb logcat Test:I |
|修改日志缓存 | adb shell logcat -G  5M |
|查看日志缓存 | adb shell logcat -g |
|打印奔溃日志 | adb shell logcat -v threadtime -b crash |

## 过滤日志
### （1）过滤特定内容的日志
输入： ^(.*(XXX|YYY)).*$

其中：
^ 匹配字符串开始位置
. 匹配除换行符 \n 之外的任何单字符
* 匹配前面的子表达式零次或多次
() 表示一个字表达式的开始与结束

| 指明两项之间的一个选择，可以理解为或，多个内容可依次添加
$ 匹配字符串结束位置

### （2）屏蔽特定内容的日志

输入： ^(?!.*(AAA|BBB)).*$
其中：
?! 表示非捕获元，匹配后面不是我们指定的内容的字符

## ps
执行 adb shell ps | grep adbd ，可以找到该后台进程，windows 请使用 findstr 替代 grep

## input

adb shell input keyevent 键名

或者不需要加前缀KEYCODE_也可以

adb shell input text +具体内容    发送文本内容，不能发送中文 

adb shell input tap x y 点击事件

adb shell input swipe 800 600 100 600 滑动事件  例如：从右往左滑动屏幕 

双击
adb shell "input tap 1631 51 & input tap 1631 51"
双击20次
adb shell “seq 20 | while read i;do input tap 350 850 & input tap 350 850 & sleep 0.3;done”

## screencap
adb shell screencap -p /sdcard/DCIM/screenTest.png
## screenrecord
adb shell screenrecord /sdcard/demo.mp4
## ime
adb shell ime list -s 列出设备上的输入法 

## 重启adb
adb kill-server

adb start-server





### 杀对应的进程
netstat -aon|findstr “5554”
tasklist|findstr “18956”
taskkill /T /F /PID 18956


遇到da重复重启时，试一下输入这个命令：adb shell setprop persist.sys.disable_rescue true


## 录制屏幕
```bat
#!/bin/sh
echo %time%
echo %date%
#小时暂时不要
set h=%time:~0,2%
set name=%date:~0,4%%date:~5,2%%date:~8,2%%time:~3,2%%time:~6,2%.png
echo %name%
adb shell /system/bin/screencap  -p  /sdcard/%name%
adb pull /sdcard/%name% D:\screenrecord/
WS
```


## setting
开启 Dark Mode: adb shell settings put secure ui_night_mode 2

关闭 Dark Mode: adb shell settings put secure ui_night_mode 1

## monkey
adb shell monkey --throttle 100 --ignore-crashes --ignore-timeouts --ignore-security-exceptions --ignore-native-crashes --monitor-native-crashes -v -v -v 9999999 > d:\monkey.log