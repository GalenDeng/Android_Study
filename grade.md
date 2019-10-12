# grade 的 configture intro (2019/10/11)

1. `com.android.support `
```
com.android.support 是 google 做的一个版本兼容包。

understand:
如果你在开发中使用了在高版本中才有的API特性，通过com.android.support库也可实现在低版本上使用。（appcompat-v7 即为 com.android.support 中的其中一个库。）

使用 appcompat-v7 是为了保证编译的 apk 能够保持向下兼容，所以 appcompat-v7 的版本必须和 compileSdkVersion 保持一致。如果 appcompat-v7 版本小于 compileSdkVersion，则不能保证到所有版本的兼容性。如果 appcompat-v7 版本大于 compileSdkVersion，则会出现错误
```
2. ` support : v4 v7 v13`
```
v4 v7 v13
1. 概述

Google为了在较低版本中兼容高版本的控件和布局以及相关的一些主题（Theme），推出了兼容包，方便开发人员在较低版本中使用高版本的效果。

    support-v4 ： 该系列包用在API Level 4（即Android 1.6）或者更高版本以上。它包含了相对于正常SDK中更多的内容。比如说：Fragment、NotificationCompat、LoadBroadcastManager、ViewPager、PageTabStrip、Loader、FileProvider等。
    support-v7 ： 该系列包是为了考虑在API level 7(Android 2.1)及以上使用高版本效果而设计的，v7包含了v4的所有效果（v7中包含v4包的，即v7依赖于v4），v7当中支持了很多新的效果，最新的版本中还支持了Material Design的多种新的布局和空间。比如说：RecyclerView、TabLayout、ToolBar、CardView等等新的包。
    support-v13 ： 该兼容包系列主要是为了兼容API level 13（Android 3.2）以上的，是为了针对于平板兼容开发的，由于平板屏幕较大，因此该系列增强的对Fragment效果的支持，使得Fragment能够在平板的各个版中兼容（一般手机开发者不用该包）。
    v14（兼容4.0及以上）系列并没有见过有使用的地方，因此这里不赘述，不过手机开发应该很少用到
    v17(兼容4.2及以上)主要是为了支持电视设备，并为电视设备提供了一系列的组件。如下：BrowseFragment， DetailFragment， PlaybasckOverlayFragment， SearchFragment 具体导入跟上面v4、v7一样。

```