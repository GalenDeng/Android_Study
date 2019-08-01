# Callable和future的使用 (2019.08.01)

1. `method`
```
    public byte[] handleText(final RemotePrinter remotePrinter, final Context context) {

        try {
            Callable<byte[]> callable = new Callable<byte[]>() {
                @Override
                public byte[] call() throws Exception {
                    byte[] data = getTextPrintByteData(remotePrinter, context);
                    return data;
                }
            };
            FutureTask<byte[]> futureTask = new FutureTask<>(callable);
            Thread thread = new Thread(futureTask);
            thread.start();
            return futureTask.get();
        } catch (Exception e) {
            e.printStackTrace();
            return null;
        }
    }

```