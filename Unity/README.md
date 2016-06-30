# 4. Unity 开发指引文档


## 简介

iMSDK Unity SDK 采用 C# 语言进行开发，并以源码的形式提供，并调用 Android 和iOS Native 代码，实现 Unity 在底层的调用。

## 渠道支持列表

| 功能 | 功能说明 | 渠道列表 |
| -- | -- | -- | 
| [登录](Module/login.md) | 授权登录 | Facebook、GooglePlay、WeChat（微信）、Guest（iMSDK游客） |
| 分享 | 分享消息 | Facebook、Google(GooglePlus)、WeChat（微信） |
| 关系链 | 邀请、获取好友列表及发送消息 | Facebook、Google(GooglePlus)、WeChat（微信） |
| 支付 | 手机支付功能 | MidasGoogle（米大师Google支付）、MidasMol（米大师MOL支付） |
| 推送 | 手机消息推送 | XG（信鸽）、XGGCM（信鸽GCM版） |

## 开始接入

完成SDK下载后，需要进行如下操作使得插件能够正常运行：

1. [下载及导入插件](download.md)
2. [设置开发环境](setupenv.md)
3. [编写代码逻辑](quickstart.md)

可以从[功能模块](Module/README.md)及[渠道配置](Channel/README.md)中找到更多信息


 

