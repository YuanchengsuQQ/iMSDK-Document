
# iMSDK 开发指引文档

## 简介

国际版iMSDK，集成了包括登录、好友、分享、支付、推送、统计海内外多个主流渠道SDK，并为业务提供多样化的增值和自助服务。 

目前平台已接入十多款业务，成功部署在多个国家、地区。

## 平台支持

| 平台 | 语言 |
| -- | -- |
| [Android](Android/README.md) | Java |
| [iOS](iOS/README.md) | C++(C98、C11) |
| [Unity](Unity/README.md) | C# |
| [C++引擎](Cpp/README.md) | C++ |

## 功能支持

| 功能 | 支持平台 | 介绍 |
| -- | -- | -- |
| 登录 | [Android](Android/Module/Push.md), [iOS](iOS/Module/Push.md), [Unity](Unity/Module/Push.md), [C++](Cpp/Module/Push.md) | 提供授权信息，为游戏登录提供支持 |
| 分享 | [Android](Android/Module/Push.md), [iOS](iOS/Module/Push.md), [Unity](Unity/Module/Push.md), [C++](Cpp/Module/Push.md) |统一接口调用三方SDK进行分享，如：分享微信朋友圈 |
| 好友 | [Android](Android/Module/Push.md), [iOS](iOS/Module/Push.md), [Unity](Unity/Module/Push.md), [C++](Cpp/Module/Push.md) |邀请好友，获取好友列表及向好友发送消息等功能 |
| 支付 | [Android](Android/Module/Push.md), [iOS](iOS/Module/Push.md), [Unity](Unity/Module/Push.md), [C++](Cpp/Module/Push.md) |集成米大师（Midas）海外支付功能 |
| 推送 | [Android](Android/Module/Push.md), [iOS](iOS/Module/Push.md), [Unity](Unity/Module/Push.md), [C++](Cpp/Module/Push.md) |提供信鸽等消息推送机制

## 接入步骤

1. 申请iMSDK Game ID
   
   进入iTop官网业务接入页面：[https://open.itop.qq.com/app/first](https://open.itop.qq.com/app/first/)，填写相关信息并等待iMSDK结果通知
   
2. 申请需要接入渠道平台

  开发者需要自行到需要接入的渠道平台申请开发者账号及应用信息，常见接入渠道请点击[应用申请地址列表](Pre/ChannelLink.md)查看

3. 下载iMSDK

  请进入iTop官网业务下载界面：[https://open.itop.qq.com/download](https://open.itop.qq.com/download)，选择游戏需要的SDK进行下载

4. 开始接入

  可以根据对应的平台指引文档进行开发，快速入口：
  
  * [Android 快速开发指引](Android/quickstart.md)
  * [iOS 快速开发指引](iOS/quickstart.md)
  * [Unity 快速开发指引](Unity/quickstart.md)
  * [C++ 快速开发指引](Cpp/quickstart.md)

## 联系我们

| 业务 | 联系人 |
| -- | -- |
| 业务接入 | [kerenwang](kerenwang@tencent.com) |
| Android SDK | [aeonyang](aeonyang@tencent.com) |
| iOS | [brightwan](brightwan@tencent.com) |
| Unity | [aeonyang](aeonyang@tencent.com) |
| 服务器 | [hirryli](hirryli@tencent.com) |









