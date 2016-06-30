# 4.4.1 登录模块(Login)

## 命名空间

```cs
using Tencent.iMSDK
```

## 接口类

```cs
IMSDKApi.Login
```

<font color=red>该类自动绑定在Unity的Tencent.iMSDK.IMLogin（GameObject）上，开发者不要主动销毁该对象！</font>

## 模块使用说明

该模块主要是用于用户认证，获取用户的基本资料

### 基本登录

iMSDK调用登录功能十分简单，一般只需要调用三个函数即可

```cs
// 初始化功能模块
IMSDKApi.Login.Initialize();

// 设定渠道
IMSDKApi.Login.SetChannel("Facebook");

void OnLogin(IMLoginResult loginResult) {
  if(loginResult.RetCode == 1) {
    // TODO
    Debug.Log("user name : " + loginResut.GuidUserNick);
    Debug.Log("open id : " + loginResut.OpenId);
    Debug.Log("iMSDK token : " + loginResut.GuidToken);
  }
  else {
    // TODO
    
  }
}
// 调用登录
IMSDKApi.Login.Login();

```

### 多登陆态共存说明

iMSDK支持多登陆态共存，如:

```cs
// Facebook 登陆
IMSDKApi.Login.SetChannel("Facebook");
IMSDKApi.Login.Login();

// WeChat 登陆
IMSDKApi.Login.SetChannel("WeChat");
IMSDKApi.Login.Login();
```
    
如果两次登陆都成功的话，那么本地会有两个有效的登录态，可以通过SetChannel方法进行切换。

```cs
// 获取 Facebook 登陆数据
IMSDKApi.Login.SetChannel("Facebook");
IMLoginResult facebookLoginResult = IMSDKApi.Login.GetLoginResult();

// 获取 WeChat 登陆数据
IMSDKApi.Login.SetChannel("WeChat");
IMLoginResult wechatLoginResult = IMSDKApi.Login.GetLoginResult();
```

同样，登出时也需要根据渠道进行登出。



### 绑定功能说明

iMSDK提供了一套账号绑定机制，可以实现不同渠道的账号关联。

绑定另外一个渠道之前，必须先登录一个渠道

```cs
// 先登录到游客
IMSDKApk.Login.SetChannel("Guest");
IMSDKApi.Login.Login();

...

// 绑定到Facebook
IMSDKApi.Login.Bind("Facebook");
```

<font color=red> 注意：</font>

1. 绑定之后，需要特别留意回调返回值，OpenID不变，但Token会发生变化，需要注意刷新游戏服务器后台的Token，避免出现后台Token失效的情况 ！
2. 绑定返回数据可以能是原渠道数据，也有可能是目标渠道数据，可根据游戏需要进行配置，这一点需要特别小心！


### 本地登录态失效说明

<font color=orange>登录数据是有有效期的，游戏后台需要判断iMSDK的登录态</font>

QuickLogin及GetLoginResult是根据本地保存数据进行判断的，可能出现登录态失效的情况，所以，游戏服务器后台必须与iMSDK后台校验登录态。

示例伪代码：

```cs
// 游戏启动时初始化
IMSDKApi.Login.Initialize();

...

// 快速登录回调处理
void OnQuickLogin(IMLoginResult result) {
    // 快速登录成功
    if(result.RetCode == 1) {
        // 连接到服务器
        int ret = ConnectToGameServer(result.OpenId, result.GuidToken, ...);
        // 如果服务器返回校验登录态失败
        if(ret == RET_SERVER_LOGIN_DATA_EXPIRED) {
            //登出清理本地数据
            IMSDKApi.Login.Logout();
            //提示用户
            if(ConfirmToCallLogin()) {
                IMSDKApi.Login.Login(OnLogin);
            }
            else{
                ...
            }
        }
    }
    // 快速登录失败
    else {
        ...
    }
}

...

// 设定渠道获取登录数据
IMSDKApi.Login.SetChannel("Facebook");
// 使用快速登录
IMSDKApi.Login.QuckLogin(OnQuickLogin);
...
```

### 子渠道登录说明

部分渠道集成了许多子渠道，在调用登录组件时，需要指定子渠道，iMSDK 侧通过调用设定子渠道来调用相应的登录功能

```cs
IMSDKApi.Login.SetChannel("Garena");
IMSDKApi.Login.SetLoginType("GRN_FB");
IMSDKApi.Login.Login(OnGaranaFacebookLogin);
```

子渠道可以在“渠道使用说明”章节中找到

### 严格登录说明

严格登录(StrictLogin)是指，只有注册或者绑定用户才能登录成功，该功能可以实现登录是依附于一个基础账号的需求。

应用场景如下：
1. 游戏进入时没有登录界面，直接用一个渠道登录，如游客（Guest）
2. 在游戏中，提供一个绑定界面，可以绑定到其他社交渠道
3. 绑定完成后，可以用StrictLogin进行登录
4. 如果社交渠道尚未注册，调用该方法会返回失败


### 上报状态功能说明

部分渠道支持状态上报功能（类似QQ在线状态），可以通过上报修改玩家的状态

调用逻辑：
1. 设定上报渠道
2. 上报状态，如“正在玩游戏”
3. 游戏退出或类似状态，取消上报


## 工程配置说明

### Android工程配置说明

> 主要需要修改Assets/Plugins/Android/AndroidManifest.xml文件，具体内容可参考渠道功能文档。

### iOS工程配置说明

> 主要需要修改目标iOS工程plist文件、IMSDKAppSetting.bundle文件中的配置，具体内容可参考渠道功能文档。


## 参考

* 登录返回结构体 <font color=blue>IMLoginResult</font>

| 变量 | 说明 |
| -- | -- |
| public int RetCode | 登录状态码，1 为成功登录，其他为失败 |
| public string ErrorMsg | 错误信息 |
| public int ChannelId | iMSDK 渠道 ID ，如：Facebook的渠道 ID 为 1 |
| public string Channel | 当前登录渠道，如：Facebook |
| public int GameId | iMSDK 游戏 ID，如：1010 |
| public string OpenId | OpenId，用户游戏账号，在游戏内应该使用该字段作为用户标识 | 
| public string Guid | 用户全局ID，IMSDK提供的用户标识，在多款游戏中可以定位到用一个用户的 ID |
| public string GuidToken | iMSDK 后台使用的Token，与 OpenId 配合使用 |
| public uint GuidTokenExpire | GuidToken 有效时间，从北京时间1970年01月01日08时00分00秒的时间戳 |
| public string GuidUserNick | 用户昵称 |
| public string GuidUserBirthday | 用户生日，如：1990-01-01 |
| public int GuidUserSex | 用户性别，0-未知；1-男；2-女 |
| public string GuidUserPortrait | 用户头像地址 |
| public List< string > ChannelPermissions | 用户已有权限列表，部分渠道无法获取改字段 |

* 回调代理函数 <font color=blue>LoginCallback</font>

| 类型 | 说明 |
| -- | -- |
| public delegate void LoginCallback(IMLoginResult result);  | 登录回调函数，返回登录结果结构体 |

* 用户绑定资料结构体 <font color=blue>IMBindInfo</font>

| 类型 | 说明 |
| -- | -- |
| public string ChannelId | iMSDK 渠道 ID ，如：Facebook的渠道 ID 为 1 |
| public string GuidUserName | 用户昵称 |
| public int GuidUserSex | 用户性别，0-未知；1-男；2-女 |
| public String GuidUserPortrait | 用户头像地址 |

* 绑定查询返回结构体 <font color=blue>IMBindInfoResult</font>

| 变量 | 说明 |
| -- | -- |
| public int RetCode | 登录状态码，1 为成功登录，其他为失败 |
| public string ErrorMsg | 错误信息 |
| public int ChannelId | iMSDK 渠道 ID ，如：Facebook的渠道 ID 为 1 |
| public int GameId | iMSDK 游戏 ID，如：1010 |
| public string OpenId | OpenId，用户游戏账号，在游戏内应该使用该字段作为用户标识 | 
| public string Guid | 用户全局ID，IMSDK提供的用户标识，在多款游戏中可以定位到用一个用户的 ID |
| public string GuidToken | iMSDK 后台使用的Token，与 OpenId 配合使用 |
| public uint GuidTokenExpire | GuidToken 有效时间，从北京时间1970年01月01日08时00分00秒的时间戳 |
| public string GuidUserNick | 用户昵称 |
| public string GuidUserBirthday | 用户生日，如：1990-01-01 |
| public int GuidUserSex | 用户性别，0-未知；1-男；2-女 |
| public string GuidUserPortrait | 用户头像地址 |
| public List< IMBindInfo > InfoList | 用户绑定渠道资料 |

* 查询绑定信息代理函数 <font color=blue>BindInfoCallback</font>

| 类型 | 说明 |
| -- | -- |
| public delegate void BindInfoCallback(IMBindInfoResult result) | 查询绑定信息，返回用户登录结果列表 |

* 登录方法类 <font color=blue>IMLogin</font>

| 函数名 | 函数说明 |
| -- | -- |
| public bool Initialize() | 初始化方法，在调用其他函数之前必须需要调用该函数 |
| public bool Initialize(string channel) | 初始化，并制定登录渠道，如Facebook |
| public bool SetChannel(string channel) | 设置登录渠道，如Facebook |
| public string GetChannel() | 获取当前设定渠道 |
| public void SetType(string type) | 复杂渠道设置登录类型 |
| public void Login( <br>&emsp;&emsp;LoginCallback callback = null,<br> &emsp;&emsp;List< string > permissionList = null,<br>&emsp;&emsp;bool needGuid = true) | 一般登录<br> callback 为回调函数，默认为null<br> permissionList 权限列表，权限可以从对应的平台找到 <br> needGuid 是否需要guid，建议使用默认值为true |
| public void StrictLogin( <br>&emsp;&emsp;LoginCallback callback = null,<br> &emsp;&emsp;List< string > permissionList = null,<br>&emsp;&emsp;bool needGuid = true) | 严格登录，只有用户资料存在时才能登录成功<br> callback 为回调函数，默认为null<br> permissionList 权限列表，权限可以从对应的平台找到 <br> needGuid 是否需要guid，建议使用默认值为true |
| public void QuickLogin(LoginCallback callback = null) | 快速登录，该方法会尝使用上次登录保存的数据进行登录<br>如果之前没有登录，或者登录已经失效，将返回错误信息 |
| public bool IsLogin() | 判断用户是否已经登录 |
| public void AutoLogin(LoginCallback callback = null) | 自动登录，如果玩家之前已经登录过，就调用上一次的登录结果 |
| public IMLoginResult GetLoginResult() | 获取当前登录返回数据 |
| public void Logout() | 登出当前渠道 |
| public void Bind(string channel, LoginCallback callback = null) | 绑定到其他渠道账号<br> <font color=orange>注意：不能绑定到游客（Guest）账户</font> |
| public void GetBindInfo(BindInfoCallback callback=null) | 获取用户绑定渠道资料 |
| public void SetPlayingReportChannel(string channel) | 设定状态上报渠道 |
| public void ActivatePlayingReport(string extraJson="") | 上报状态 |
| public void DeactivatePlayingReport() | 关闭上报 |
| public bool IsChannelAppInstalled() | 是否安装渠道应用，只有部分渠道支持 |
| public bool IsChannelSupportApi() | 应用API版本是否可用，只有部分渠道支持 |

## 代码示例


```cs
void Start() {
    IMSDKApi.Login.Initialize ();
    IMSDKApi.Login.SetChannel("Facebook");
}

void TestLoginCallback(IMLoginResult result) {
    if(result.RetCode == 1) {
        Debug.Log("login ok, user open id is " + result.OpenId);
    }
    else {
        Debug.Log("login error : " + result.ErrorMsg);
    }
}

void TestLogin() {
    List<string> permissionList = new List<string>();
    permissionList.Add("email");

    IMSDKApi.Login.Login(TestLoginCallback, permissionList, true);
}
```
