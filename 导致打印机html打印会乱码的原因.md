#  导致打印机html打印会乱码的原因 (2019.09.25)
1. `导致html打印乱码原因 -- width的实现中，byte类型只支持到 -128 - 127`
```
<body style="width:245px" > 中的 width 的实现有问题

	public static byte[] marginLeft(int left){
		int nL = left % 256;
		int nH = left / 256;
		return new byte[]{ 0x1B, 0x5C, (byte) nL, (byte) nH };
	}

* android中的 byte类型的有效范围是 -128 ~ 127   
* so 我们通过修改 width 的值小于 128 ，即不会出现乱码 
```