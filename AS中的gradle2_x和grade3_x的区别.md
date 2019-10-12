# AS中的gradle2_x和grade3_x的区别 (2019.10.12)

* [gradle2.x和gradle3.x的区别](https://blog.csdn.net/yuzhiqiang_1993/article/details/78366985)

1. `compile / implement / api 的区别 `
```
* compile == api

* implementation：该依赖方式所依赖的库不会传递，只会在当前module中生效。
  api：该依赖方式会传递所依赖的库，当其他module依赖了该module时，可以使用该module下使用api依赖的库

* implementation：只能在内部使用此模块，比如我在一个libiary中使用implementation依赖了gson库，然后我的主项目依赖了libiary，那么，我的主项目就无法访问gson库中的方法。这样的好处是编译速度会加快，推荐使用implementation的方式去依赖，如果你需要提供给外部访问，那么就使用api依赖即可
 
```