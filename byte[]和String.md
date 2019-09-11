# byte[] 与 String （2019.09.11）

1. `caution`
```
一般我们要对比两个byte[]数组的content , 不建议将 byte[] 转成 String 再比较，
有时候会出现转换前后 byte[] 和 String 的 length 不相等的情况，有部分数据被优化了，所以，我们要比较数组的content,就直接用 byte 这个类型比较，而不要转成 String
再比较
```