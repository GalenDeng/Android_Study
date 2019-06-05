# 创建一张可以自主定位绘图的Bitmap

1. `method --- 绘制自主定位的Bitmap`

```
* Bitmap bmp = handleImageEffect();
```
```
    public  static Bitmap  handleImageEffect() {
        // 1mm = 7.092  <=>  android 中 mm 和 float类型的unit 的 convert
        final  double convertValue = 7.092;
        // 创建的这个bmp要比你在这个bmp绘图的图片大小大一点才行
        Bitmap bmp = Bitmap.createBitmap((int)(101*convertValue),(int)(91*convertValue),Bitmap.Config.ARGB_8888);
        // canvas 绘图的内容会绘制在bmp中
        Canvas canvas = new Canvas(bmp);
        Paint mPaint = new Paint();
        mPaint.setStyle(Paint.Style.STROKE);    // 空心设置
        // 打印内容的边框 -- 矩形 （10mm x 8mm）
        canvas.drawRect(0,0,(float)(100 * convertValue),(float)(90* convertValue),mPaint);
        mPaint.setTextSize((float)(5 * convertValue));       // 字体大小
        mPaint.setStyle(Paint.Style.FILL);      // 实体设置
        // 绘图内容
        // (30mm,30mm)处绘制 Nanjing  的内容
        canvas.drawText("Nanjing",(float)(30 * convertValue),(float)(30 * convertValue),mPaint);
        // (20mm,20mm)处绘制 南京急救中心 的内容
        canvas.drawText("南京急救中心",(float)(20*convertValue),(float)(20 * convertValue),mPaint);
        // 10mm
        canvas.drawLine(0,(float)(35*convertValue),(float)(10*convertValue),(float)(35*convertValue),mPaint);
        //20mm
        canvas.drawLine(0,(float)(45*convertValue),(float)(20*convertValue),(float)(45*convertValue),mPaint);
        //50mm
        canvas.drawLine(0,(float)(55*convertValue),(float)(50*convertValue),(float)(55*convertValue),mPaint);
        //100mm
        canvas.drawLine(0,(float)(65*convertValue),(float)(100*convertValue),(float)(65*convertValue),mPaint);
        return bmp;
    }
```