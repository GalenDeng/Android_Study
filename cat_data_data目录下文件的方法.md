# 查看 /data/data/包名/ 目录下的文件的方法 （2019/07/29）

1. `method`
```
1. adb shell
2. run-as xxx(app的包名)
3. 即可进入到 /data/data/xxx(包名)/ 目录下
```
2. `查询某个apk的包名方法`
* cd 到 SDK的 platform-tools/ 目录下
* adb shell "dumpsys window | grep mCurrentFocus" 即可查看到当前运行的apk的包名名称
