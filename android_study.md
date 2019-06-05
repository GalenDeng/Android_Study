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

4. `byte转int -> int的值以字符串输出`
```
    private String printerModel;

    byte[] bs1 = new  byte[2];
    bs1[0] = RecvData[6];
    // java总是把byte当作有符处理；我们可以通过将其和0xff进行二进制与得到它的无符值
    int galen1 = bs1[0] & 0xFF;
    bs1[1] = RecvData[7];
    int galen2 = bs1[1] & 0xFF;
    String s11 = String.valueOf(galen1) + String.valueOf(galen2);
    printerModel =  s11;
```
* byte与int转换
```
public static byte intToByte(int x) {
    return (byte)x;
}

public static int byteToInt(byte b) {
    // java总是把byte当作有符处理；我们可以通过将其和0xff进行二进制与得到它的无符值
    return b & 0xff;
}
```
* byte[] 与 int转换
```
public static int byteArrayToInt(byte[] b) { // int 是 32 位整数
    return b[3] &0xFF | (b[2] & 0xFF) << 8 | (b[1] &0xFF) << 16 | (b[0] & 0xFF) << 24 ;
}

public static byte[] intToByteArray(int a) {
    return new byte[] {
        (byte)((a >> 24) & 0xFF,
        (byte)((a >> 16) & 0xFF),
        (byte)((a >> 8)  & 0xFF),
        (byte)(a & 0xff)
    };
}
```
```
* byte，即字节，由8位的二进制组成。在Java中，byte类型的数据是8位带符号的二进制数。
* 在计算机中，8位带符号二进制数的取值范围是[-128, 127]，所以在Java中，byte类型的取值范围也是[-128, 127]
* 二进制从 00000000 到01111111到10000000到 11111111 
  即 十进制从 0 到 127 到 -128 到 -1
```

5. `获取外部文件路径`
* [Android系统用于Activity的标准Intent](https://blog.csdn.net/zhangjg_blog/article/details/10901293)
* [通过URI获取的文件路径为null的解决方法](https://blog.csdn.net/dj0379/article/details/50765021)
```
* Android 4.4 以后，打开外部存储的文件获取到的文件路径是经过处理的,不是真正的文件路径，需要经过处理
```
```
网上实例：
打开多个应用选取各种类型的数据,以uri返回。返回的uri可使用ContentResolver.openInputStream(Uri)打开
    该功能可用在邮件中附件的选取
    举例如下:
    选取一张图片, 返回的uri为 content://media/external/images/media/47
    选取一首歌, 返回的uri为 content://media/external/audio/media/51

    		Intent intent = new Intent();
    		intent.setAction(Intent.ACTION_GET_CONTENT);     
    		intent.setType("*/*");
    		intent.addCategory(Intent.CATEGORY_OPENABLE);
    		startActivityForResult(intent, 2);
```
* `真实用例`
```
case xxx.button:
    // 创建 Intent 对象，进行通信
    Intent chooseIntent = new Intent(Intent.ACTION_GET_CONTENT);
    chooseIntent.setType("*/*");    // 设置可以打开的文件类型
    chooseIntent.addCategory(Intent.CATEGORY_OPENABLE); // 指定返回的uri可使用ContentResolver.openInputStream（Uri）打开
    startActivityForResult(Intent.createChooser(chooseIntent,"用于图片打开")，1)；

    // startActivityForResult 方法得到结果后会回调 onActivityResult 方法，进行下一步的操作
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        if (resultCode == RESULT_OK) {
            switch (requestCode) {
                case 0:
                    // 获取外部存储文件的路径 ： 注意 Android 4.4 以后得到的文件路径不是真正的
                    // 需要对获取的文件路径进行进一步操作才能获取到路径
                    String filePath = getFilePath(this, data.getData());
                    if (filePath == null) {
                        ToastUtil.show(this, getString(R.string.file_open_failure));
                        return;
                    }
                    System.out.println(filePath);
                    int number = 0;
                    byte[] buffer = new byte[0];
                    try {
                        // 文件缓冲流读取 - 不管传入文件的格式，这里只负责传输数据罢了，和格式无关
                        DataInputStream dis = new DataInputStream(new FileInputStream(filePath));
                        int length = dis.available();
                        buffer = new byte[length];
                        number = dis.read(buffer);
                        dis.close();
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                    if (number > 0) {
                        printerManager.sendData(buffer, this);
                    } else {
                        ToastUtil.show(this, R.string.file_read_failure);
                        return;
                    }
                    break;

            }
        }
    }
```
* `对获取到的文件路径进行处理，已达到获取真实文件路径的目的`
```
 @TargetApi(Build.VERSION_CODES.KITKAT)
    public String getFilePath(Context context, Uri uri) {
        final boolean isKitKat = Build.VERSION.SDK_INT >= Build.VERSION_CODES.KITKAT;
        if (isKitKat && DocumentsContract.isDocumentUri(context, uri)) {
            System.out.println(uri);
            if (isExternalStorageDocument(uri)) {
                final String docId = DocumentsContract.getDocumentId(uri);
                final String[] split = docId.split(":");
                final String type = split[0];
                if ("primary".equalsIgnoreCase(type)) {
                    return Environment.getExternalStorageDirectory() + "/" + split[1];
                }
            }else if (isDownloadsDocument(uri)) {// DownloadsProvider
                final String id = DocumentsContract.getDocumentId(uri);
                final Uri contentUri = ContentUris.withAppendedId(Uri.parse("content://downloads/public_downloads"),
                        Long.valueOf(id));
                return getDataColumn(context, contentUri, null, null);
            } else if (isMediaDocument(uri)) {// MediaProvider
                final String docId = DocumentsContract.getDocumentId(uri);
                final String[] split = docId.split(":");
                final String type = split[0];
                Uri contentUri = null;
                if ("image".equals(type)) {
                    contentUri = MediaStore.Images.Media.EXTERNAL_CONTENT_URI;
                }
                final String selection = "_id=?";
                final String[] selectionArgs = new String[] { split[1] };
                return getDataColumn(context, contentUri, selection, selectionArgs);
            }
        } else if ("content".equalsIgnoreCase(uri.getScheme())) {
            String[] projection = {"_data"};
            try {
                Cursor cursor = context.getContentResolver().query(uri, projection, null, null, null);
                int column_index = cursor.getColumnIndexOrThrow("_data");
                if (cursor.moveToFirst()) {
                    return cursor.getString(column_index);
                }
            } catch (Exception e) {
                e.printStackTrace();
            }
        } else if ("file".equalsIgnoreCase(uri.getScheme())) {
            return uri.getPath();
        }
        return null;
    }
    public static String getDataColumn(Context context, Uri uri, String selection, String[] selectionArgs) {
        Cursor cursor = null;
        final String column = "_data";
        final String[] projection = { column };
        try {
            cursor = context.getContentResolver().query(uri, projection, selection, selectionArgs, null);
            if (cursor != null && cursor.moveToFirst()) {
                final int column_index = cursor.getColumnIndexOrThrow(column);
                return cursor.getString(column_index);
            }
        } finally {
            if (cursor != null)
                cursor.close();
        }
        return null;
    }

    public boolean isExternalStorageDocument(Uri uri) {
        return "com.android.externalstorage.documents".equals(uri.getAuthority());
    }

    public static boolean isDownloadsDocument(Uri uri) {
        return "com.android.providers.downloads.documents".equals(uri.getAuthority());
    }

    public static boolean isMediaDocument(Uri uri) {
        return "com.android.providers.media.documents".equals(uri.getAuthority());
    }

```

6. `签名区别`
```
1. V1签名适用于所有的android version ; V2签名只适用于 android 7.0及以上的 version
```
7. `系统时间获取`
```
        Calendar cal = Calendar.getInstance();
        cal.setTimeZone(TimeZone.getTimeZone("GMT+8:00"));
         
        String year = String.valueOf(cal.get(Calendar.YEAR));
        String month = String.valueOf(cal.get(Calendar.MONTH)+1);
        String day = String.valueOf(cal.get(Calendar.DATE));
        if (cal.get(Calendar.AM_PM) == 0)
            hour = String.valueOf(cal.get(Calendar.HOUR));
        else
            hour = String.valueOf(cal.get(Calendar.HOUR)+12);
        minute = String.valueOf(cal.get(Calendar.MINUTE));
        second = String.valueOf(cal.get(Calendar.SECOND));
         
        String system1 = year + "-" + month + "-" + day;
        String system2 = hour + "-" + minute + "-" + second;
```