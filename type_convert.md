# type_convert  summary -- 类型转换汇总

1. `byte 转 无符号数`
```
byte[] src = { (byte)0x01,(byte)0x02,(byte)0x03,(byte)0x04,}
int src3 = src[i+3] & 0xff;

* 在 java 中, 所有数据类型都是有符号的，要想将某数据类型的数值转成无符号数，
  通用的做法是将该类型的数值用拥有位数更多的数据类型表示，以达到无符号数的目的
  (example : byte b; int a = b & 0xff)_
```