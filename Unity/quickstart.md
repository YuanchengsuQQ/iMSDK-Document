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

**部分功能有默认渠道，可以不用指定。我们建议显示的调用SetChannel方法，让渠道字段更清晰**

## 调用代码逻辑

完成初始化之后，就可以调用相应的代码功能了，如下：

```cs
void OnFacebookLogin(IMLoginResult loginResult) {
  if(loginResult.RetCode == 1) {
    //TODO Login success
    Debug.Log("user name : " + loginResult.GuidUserNick);
    Debug.Log("openid : " + loginResult.OpenId);
    Debug.Log("iMSDK token : " + loginResult.GuidToken);
  }
  else {
    //TODO Login error
    Debug.Log("login error : " + loginResult.ErrorMsg);
  }
}

void HandleTouchEvent() {
  List<string> permissionList = new List<string> ();
  permissionList.Add ("user_friends");
  IMSDKApi.Login.Login (OnFacebookLogin, permissionList);
  IMSDKApi.Login.Login()
}
```
