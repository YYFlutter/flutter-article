# AssetBundle

## 介绍

asset——资源，AssetBundle是一个用来加载资源的抽象类，其子类有以下三个：
*DefaultAssetBundle
*NetworkAssetBundle
*rootBundle
在程序中，我们可以通过这三个子类来实现各种情况下的资源加载。

在之前的Image Demo里面，我们是通过AssetImage()来加载图片资源的，而在AssetImage中：
```dart
  const AssetImage(this.assetName, {
    this.bundle,
    this.package,
  }) : assert(assetName != null);
//......
@override
  Future<AssetBundleImageKey> obtainKey(ImageConfiguration configuration) {
    final AssetBundle chosenBundle = bundle ?? configuration.bundle ?? rootBundle;
    Completer<AssetBundleImageKey> completer;
    Future<AssetBundleImageKey> result;
```
其根本还是通过AssetBundle来加载的。

## 使用

在程序中，我们用的最多的还是静态资源，可以打包到程序中，随时可用。
在Flutter中，如果要使用静态资源，需要在pubspec.yaml文件中先行配置：
```dart
flutter:
  assets:
    - images/my_icon.pngxian
    - images/
    - assets/
```
在高版本中，不用每个文件都进行配置，只需要配置到资源文件夹就行。 
但是，如果要想资源像Android原生那样，在不同的环境下加载不同资源，便需要按照固定的格式进行配置。

比如有以下两个文件：
```
.../img/background.png
.../img/dark/background.png
```
如果pubspec.yaml 配置为：
```dart
flutter:
  assets:
    - img/background.png
```
那么 img/background.png 和 img/dark/background.png 将包含在 asset bundle 中。
前者被认为是 main asset，后者被认为是一种变体 variant。
可以通过这种特性，来实现不同屏幕加载不同分辨率的图片：将不同分辨率的图片放在不同的倍率文件下，比如：
./xx/2.0x/xxx.png
./xx/3.0x/xxx.png

如果pubspec.yaml 配置为：
```dart
flutter:
  assets:
    - img/
```
那么 img/background.png 和 img/dark/background.png 将包含在 asset bundle 中。
可以通过 AssetImage('img/background.png') 和 AssetImage('img/dark/background.png') 分别引用

上面提到过AssetBundle的三个子类，在每个Flutter应用程序都有一个 rootBundle 对象，可以直接用来访问 main asset bundle。
但是最好使用 DefaultAssetBundle 来获取当前 BuildContext 的 AssetBundle。
这种方法不是使用应用程序构建的默认 asset bundle，而是使父级 widget 在运行时替换的不同的 AssetBundle，这对于本地化或测试场景很有用。
通常，可以使用 DefaultAssetBundle.of() 从应用运行时间接加载asset。



