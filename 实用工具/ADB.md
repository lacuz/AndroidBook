# ADB

window下shell后面尽量加双引号

adb reverse tcp:8081 tcp:8081 释放端口


adb shell uiautomator dump /sdcard/ui.xml 获取手机屏幕布局信息




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

## dumps
查看当前设备所运行的包名 ，activity名

adb shell dumpsys window w | findstr name | findstr \/


## getprop
获取系统版本
adb shell getprop ro.build.version.sdk
查看设备重启的原因
adb shell getprop sys.boot.reason

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


## input

adb shell input keyevent 键名

或者不需要加前缀KEYCODE_也可以

adb shell input tap x y 点击事件

双击
adb shell "input tap 1631 51 & input tap 1631 51"
双击20次
adb shell “seq 20 | while read i;do input tap 350 850 & input tap 350 850 & sleep 0.3;done”
