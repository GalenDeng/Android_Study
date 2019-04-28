## android_study (2019.1.29)
*  `android 整理代码快捷键` ： `ctrl + alt + L`
*  `返回到上一次浏览的页面位置`： `ctrl + alt + ← `,而mac电脑是 `command + alt + ← `

*  `加载project的时候报 migrate project to the gradle 的解决方法`
```
* 先备份工程
1.close project;
2.删除项目工程下的.idea文件夹,以及所有的.iml文件;
3.import project,在选择文件中 选中项目根目录下的 build.gradle.
4.等待AS自动编译到完成,时间较长;
```
2. `出现 com.android.id.library not be found 的解决方式`
```
* 在 gradle.build file的最上面添加以下代码:

apply plugin: 'com.android.library'

buildscript {
repositories {
jcenter()
google()
}
dependencies {
classpath 'com.android.tools.build:gradle:3.2.1'
//注意：更换成自己的AS的版本
}
}
allprojects {
repositories {
jcenter()
}
}
```

3. `android studio + gradle 生成jar文件`
* `基本常识`
```
apply plugin: 'com.android.library' 
# write library 表示的是生成的是库，而改成 application 表示的是一个应用程序

# 仓库等指定 --- 有些AS的版本比较低，并没有 buildscript 来指定，导致 com.android.library not found
# 故要在 apply plugin: 'com.android.library' 后 添加以下的程序

buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:2.3.3'
        //注意：更换成自己的AS的版本
    }
}
allprojects {
    repositories {
        jcenter()
    }
}
```
* `混淆与合并`
```
1. 
* 在Android Studio 中 run build ,会在app目录下生成一个class.jar库文件
目录为:  build/intermediates/bundles/debug/ or build/intermediates/bundles/release
* 这个class.jar 是没有混淆过的jar文件
* 当我们给第三方使用这个库时，要使其混淆，我们这里可以使用 proguard-rules.pro 这个文件进行编写库的混淆规则 
* 当我们编写好 proguard-rules.pro 这个混淆规则文件后 -> sync project with Gradle Files -> click 右侧 
gradle -> select  项目名称/Tasks/others/makeJar
* 有时候我们通过makeJar解决不了问题的时候，我们可以使用 windows 端 retroguard 进行混淆 ，使用 apache-ant-1.10.1 进行合并 
```
```
2.混淆
* [jar的混淆](https://www.softpedia.com/get/Programming/Other-Programming-Files/RetroGuard.shtml)
* cd xxxPackage/混淆/retroguard
java RetroGuard classes.jar printerlib.jar script_3_4.rgs
```
```
3. apache-ant 的 install and use
* [apache-ant install reference](https://blog.csdn.net/song_hui_xiang/article/details/14315529)
* source ~/.bashrc : 使到 /etc/bashrc 的内容生效

* 具体步骤
1） 官网(http://ant.apache.org/bindownload.cgi)下载xxx.bin.zip格式的ant文件： apache-ant-1.10.5-bin.zip
2) 将这个zip压缩包解压后放到 /usr/local
3) ln -s apache-ant-1.10.5-bin ant : 做一个链接link
4) sudo vim /etc/bashrc -> 在 content 最后 add 
    export ANT_HOME=/usr/local/ant
    export PATH=${PATH}:${ANT_HOME}/bin
5) .wq!
6) source ~/.bashrc
7) cmd 中 输入命令 ant -version 来证明ant是否已经install successful
8) 在desktop 中 按 windows 的操作进行一遍就可以实现合并了 【build.xml】
   ant -buildfile /Users/admin/Desktop/Package/jar/apache-ant-1.10.5/build.xml
```


3. `查看 .so接口函数的命令`
```
* nm -D xxx.so
```

