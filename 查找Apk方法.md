# 查找apk的方法 （2019.01.09）

1. `adb 取出安装在手机中的 apk`
* [adb 取出安装在手机中的 apk](https://blog.csdn.net/think_ycx/article/details/84064019)
* adb shell pm list packages    // 列出installed 的应用包名
* adb shell pm path  包名(com.jolimark.android.printservice)  // 查找相关apk的位置
* adb pull /xxx.apk   /yyy  // 拉apk 出来