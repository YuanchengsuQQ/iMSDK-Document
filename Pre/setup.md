# 1.1 基础准备
## 基础知识

在接入iMSDK之前，需要了解iMSDK的几个基本知识

1. 什么是插件化？
  
  iMSDK由三分部组成：
  
  * 基础包，主要是提供统一接口、封装基础方法和通用方法，是其他功能的基础
  
  * 插件包，iMSDK所有的功能模块都是以插件（Plugin）的模式提供，也是iMSDK最重要的组成部分
  
  * 扩展包，在iMSDK框架之外的功能，我们以扩展模块的形式提供

  在这种框架下，任何的功能都可以以插件的模式进行添加、删除
  
2. 什么是渠道？

  iMSDK把一个功能平台定义为一个渠道，如：Facebook、WeChat（微信）等都是一种渠道

3. 什么是 iMSDK 的 Game ID ？

  iMSDK Game ID 是 iMSDK来标记一个业务的ID，一般来说，如果业务在不同区域发行不同的版本，那业务在每个区域应该有不同的Game ID
 
  Game ID 在接入 iMSDK时，由iMSDK进行分配

## 平台支持

目前，我们支持Android、iOS两大移动平台，并提供Unity、C++版本的接口封装

** 需要注意的是，我们并不是全平台支持，目前iMSDK只支持Android、iOS两大移动平台**

| 平台 | 语言 | 备注 |
| -- | -- | -- |
| [Android](Android/README.md) | Java | - |
| [iOS](iOS/README.md) | C++(C98、C11) | - |
| [Unity](Unity/README.md) | C# | 只支持Android、iOS手机平台 |
| [C++引擎](Cpp/README.md) | C++ | 只支持Android、iOS手机平台 |

## 功能支持

iMSDK按常见的接入功能分成如下常见功能模块：

| 功能 | 支持平台 | 介绍 |
| -- | -- | -- |
| 登录 | [Android](Android/Module/Push.md), [iOS](iOS/Module/Push.md), [Unity](Unity/Module/Push.md), [C++](Cpp/Module/Push.md) | 提供授权信息，为游戏登录提供支持 |
| 分享 | [Android](Android/Module/Push.md), [iOS](iOS/Module/Push.md), [Unity](Unity/Module/Push.md), [C++](Cpp/Module/Push.md) |统一接口调用三方SDK进行分享，如：分享微信朋友圈 |
| 好友 | [Android](Android/Module/Push.md), [iOS](iOS/Module/Push.md), [Unity](Unity/Module/Push.md), [C++](Cpp/Module/Push.md) |邀请好友，获取好友列表及向好友发送消息等功能 |
| 支付 | [Android](Android/Module/Push.md), [iOS](iOS/Module/Push.md), [Unity](Unity/Module/Push.md), [C++](Cpp/Module/Push.md) |集成米大师（Midas）海外支付功能 |
| 推送 | [Android](Android/Module/Push.md), [iOS](iOS/Module/Push.md), [Unity](Unity/Module/Push.md), [C++](Cpp/Module/Push.md) |提供信鸽等消息推送机制
