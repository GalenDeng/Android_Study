# android_APP搜索相同的wifi打印机出来的解决方法 （2019.09.25）

1. `the way to resolve the question`
```
				@Override
						public void deviceFound(DeviceInfo deviceInfo) {
							if (!(wifiList.contains(deviceInfo))) {
						wifiList.add(deviceInfo);
						Log.d("WifiList", String.valueOf(deviceInfo));
						mHandler.sendEmptyMessage(ErrorOrMsg.DEVICE_FOUND);
						// 因为sendEmptyMessage 是 异步回调处理，为防止 wifiList.add 的device 多了，需要加一点 delay time
						// 这次测试 30ms延时即可
						try {
							Thread.sleep(100);
						}catch (Exception e) {
							e.printStackTrace();
						}
					}
				}
```