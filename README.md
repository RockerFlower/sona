![logo](./arts/logo.png)![pub package](https://img.shields.io/pub/v/sona.svg)

sona makes possible using getui push in flutter.

## 简介
`Sona`是个推推送SDK在`Flutter`上的实现。通过`Sona`,可以在Flutter上轻松使用个推推送。
使用`Sona`之前，请到个推官网进行应用注册。

## 所用到的技术
android使用到了*kotlin-1.3.11*：
```groovy
dependencies {
    implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk7:$kotlin_version"
    api 'com.getui:sdk:2.12.5.0'
}

```
iOS上：
```ruby
  s.dependency 'GTSDK'
  s.ios.deployment_target = '8.0'
```
Flutter上：
```dart
Flutter 1.0.0 • channel beta • https://github.com/flutter/flutter.git
Framework • revision 5391447fae (4 weeks ago) • 2018-11-29 19:41:26 -0800
Engine • revision 7375a0f414
Tools • Dart 2.1.0 (build 2.1.0-dev.9.4 f9ebf21297)
```
## 初始化
鉴于`Android`和`iOS`的差异化，对应平台设置还需手动设置，具体请参考[官网](http://docs.getui.com/getui/mobile/android/androidstudio_maven/)。
在`Flutter`中通过`Sona`初使化个推推送:
```dart
    import 'package:sona/sona.dart' as sona;
    sona.register(
        appID: "your app id",
        appKey: "your app key",
        appSecret: "app secret"
    );
```
`appID`，`appKey`，`appSecret`目前仅在`iOS`上生效，因为在`android`上，这些配置是在`build.gradle`中完成的，所以使用`Sona`之前
一定要在`android`工程配置`appID`、`appKey`以及`appSecret`：
```
defaultConfig {
        //some configrations

        manifestPlaceholders = [
                GETUI_APP_ID : "APP_ID",
                GETUI_APP_KEY : "APP_KEY",
                GETUI_APP_SECRET : "APP_SECRET"
        ]
    }
```

## 接收透传
通过监听`receivedMessageData`可以获取个推推送的透传数据：
```dart
   sona.receivedMessageData.listen((payload){
      //接收到透传
      });
```
其中*payload*为`Map<dynamic,dynamic>`根据平台不台，其包含的key也不同：
- appID:String
- taskID:String
- messageID:String
- offLine:bool
- payload:String or null
- pkgName:String,仅安卓平台


