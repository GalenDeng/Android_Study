# array copy (2019.09.11)
```
    // byte数组复制
    boolean byteCmp(byte[] src1,byte[] src2,int srcbeginindex,int count) {
        boolean is_blank = false;
        byte dest[] = new byte[count];
        System.arraycopy(src1, srcbeginindex, dest, 0, count);
        is_blank = Arrays.equals(dest, src2);
        return  is_blank;
    }
```