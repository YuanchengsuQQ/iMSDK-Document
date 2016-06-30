# 4.3 快速集成指南

在完成[开发环境配置](setupenv.md)和[渠道配置](Channel/README.md)后，就可以开始编写相关代码了

我们以登录组件为例，演示iMSDK代码使用方法

## 初始化功能插件

在调用其他方法之前，必须先初始化功能插件，可以写在 Unity 的Start方法中，代码参考如下：

```cs
void Start() {
  IMSDKApi.Login.Initailize();
}
```

## 指功能渠道

初始化完成后，需要指定渠道以选择功能平台，代码参考如下：

```cs
 IMSDKApi.Login.SetChannel("Facebook");
```