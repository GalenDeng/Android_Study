# pdf转图片 （2019.08.02）

1. `Method`
```
ImageView iv_invoice = holder.getView(R.id.iv_invoice);
//初始化PdfRender
ParcelFileDescriptor mDescriptor = null;
PdfRenderer mRenderer = null;
try {
    mDescriptor = ParcelFileDescriptor.open(new File(invoicePath), ParcelFileDescriptor.MODE_READ_ONLY);
    if (mDescriptor != null) {
        mRenderer = new PdfRenderer(mDescriptor);
    }
    PdfRenderer.Page currentPage = mRenderer.openPage(0);
    Bitmap bitmap = null;
    bitmap = Bitmap.createBitmap(DisplayUtil.dp2px(800), DisplayUtil.dp2px(500), Bitmap.Config.ARGB_8888);
    currentPage.render(bitmap, null, null, PdfRenderer.Page.RENDER_MODE_FOR_DISPLAY);
    printBitmap = BitmapUtil.rotateBitmap(bitmap, 90);
    iv_invoice.setImageBitmap(bitmap);
    //关闭当前Page对象
    currentPage.close();
} catch (Exception e) {
    e.printStackTrace();
} finally {

}


ByteArrayOutputStream baos = new ByteArrayOutputStream();
printBitmap.compress(Bitmap.CompressFormat.PNG, 100, baos);
InputStream isBm = new ByteArrayInputStream(baos.toByteArray());
printerManager.close();
printerManager.sendData(PrintContent.getPicByteData(TransactionQueryListActivity.this, isBm), TransactionQueryListActivity.this);
```
```
上面的pdf转图片打印的实质是： 获取 pdf的路径 -> new File -> new PdfRenderer -> 一页一页地 open -> PdfRenderer.Page.render 把每一页的内容draw 到 bitmap -> bitmap.compress 到 ByteArrayOutputStream -> 这个流里面的数据就是每一页的内容
```