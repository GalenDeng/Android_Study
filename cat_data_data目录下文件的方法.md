# 查看 /data/data/包名/ 目录下的文件的方法 （2019/07/29）

1. `method`
```
1. adb shell
2. run-as xxx(app的包名)
3. 即可进入到 /data/data/xxx(包名)/ 目录下
```
2. `查询当前运行的app的包名方法`
* cd 到 SDK的 platform-tools/ 目录下 [windows系统]
* adb shell "dumpsys window | grep mCurrentFocus" 即可查看到当前运行的apk的包名名称

3. `查看jniLibs目录下的so文件在手机的install dir`
* Full path to the directory where native JNI libraries are stored
* String pathDisplay = getContext().getApplicationInfo().nativeLibraryDir;

4. 安装apk的方式
```
* adb install  app-debug.apk    // 普通 install
* adb install --abi armeabi-v7a app-debug.apk // 指定以32位架构install
* adb install --abi arm64-v8a app-debug.apk // 指定以64位的架构install

```
