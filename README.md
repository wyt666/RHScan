### RHScan——实现二维码扫描功能，含各种UI、手势放大缩小镜头、仿微信扫码放大
### [ iOS 模仿微信扫描二维码放大功能](http://blog.csdn.net/sinat_30336277/article/details/79314472) 

---
> 说明
> 本程序仅供学习交流，不可用于任何商业用途。

### Installation with CocoaPods
***
```ruby
pod 'RHScan'
```

我们知道，微信扫描二维码过程中，如果二维码图片焦距比较远，会拉近焦距，实现放大功能。这种效果如何该实现，用原生的API又是如何实现。本文简单尝试如何使用AVFoundation实现放大二维码图片。重点是如何定位二维码和放大二维码，前面介绍了 iOS 扫描二维码实现手势拉近拉远镜头[ iOS 识别过程中描绘二维码边框 ](http://blog.csdn.net/sinat_30336277/article/details/79295025) 和[iOS 识别过程中描绘二维码边框 ](http://blog.csdn.net/sinat_30336277/article/details/79276113) ，我们可以很简单的实现二维码定位和放大。

```
- (void)changeVideoScale:(AVMetadataMachineReadableCodeObject *)objc
{
NSArray *array = objc.corners;
CGPoint point = CGPointZero;
int index = 0;
CFDictionaryRef dict = (__bridge CFDictionaryRef)(array[index++]);
// 把点转换为不可变字典
// 把字典转换为点，存在point里，成功返回true 其他false
CGPointMakeWithDictionaryRepresentation(dict, &point);
NSLog(@"X:%f -- Y:%f",point.x,point.y);
CGPoint point2 = CGPointZero;
CGPointMakeWithDictionaryRepresentation((__bridge CFDictionaryRef)array[2], &point2);
NSLog(@"X:%f -- Y:%f",point2.x,point2.y);
CGFloat scace =150/(point2.x-point.x); //当二维码图片宽小于150，进行放大
if (scace > 1) {

[self setVideoScale:scace];
}
return;
}
```
上面代码实现检测二维码边长小于150时，进行放大。具体可以根据需求设置，并实现二维码位置的调整。


## 喜欢的朋友希望可以给个 Star，十分感谢您的支持！~
