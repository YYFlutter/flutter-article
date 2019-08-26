# RawImage

## 介绍

在看RawImage之前，我们先看看Image的build()方法：
```dart
@override
  Widget build(BuildContext context) {
    final RawImage image = RawImage(
      image: _imageInfo?.image,
      width: widget.width,
      height: widget.height,
      scale: _imageInfo?.scale ?? 1.0,
      color: widget.color,
      //......
    );
    if (widget.excludeFromSemantics)
      return image;
    return Semantics(
      container: widget.semanticLabel != null,
      image: true,
      label: widget.semanticLabel == null ? '' : widget.semanticLabel,
      child: image,
    );
  }
```
没错，Image的内部其实是通过RawImage实现的，Image其实是对RawImage进行了一次封装，遮盖了更多的细节，方便给人使用

## 构造函数

```dart
const RawImage({
    Key key,
    this.image,
    this.width,
    this.height,
    this.scale = 1.0,
    this.color,
    this.colorBlendMode,
    this.fit,
    this.alignment = Alignment.center,
    this.repeat = ImageRepeat.noRepeat,
    this.centerSlice,
    this.matchTextDirection = false,
    this.invertColors = false,
    this.filterQuality = FilterQuality.low,
  }) : assert(scale != null),
       assert(alignment != null),
       assert(repeat != null),
       assert(matchTextDirection != null),
       super(key: key);
```

这里，只对Image没有的属性进行说明，与Image相同的属性请查看[Image类](./Image类.md)

### ui.Image image
虽然Image与RawImage 的第一个参数都是image，但却是不同的，前者是Material下的Image，后者是dart：ui下的Image

### bool invertColors
invertColors是一个Image没有的属性，可以用来反转颜色




