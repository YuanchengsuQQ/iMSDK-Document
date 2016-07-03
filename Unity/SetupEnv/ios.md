# 4.2.2 iOS 环境配置

iOS的所有配置，都需要在Unity中编译导出XCode工程后，在XCode工程进行配置

### 编译选项

  在XCode工程 -> Build Settings -> Linking -> Other Linker Flags 中，添加如下编译选项：
  
  ```sh
  -all_load
  ```
  ![XCode配置编译选项](Images/4_2_unity_setupenv_xcode_all_load.jpg)
  
  如果遇到Bitcode报错（Unity 4.x版本不支持），可以通过在XCode工程 -> Build Settings -> Build Options -> Enable Bitcode 中，将值修改为No

#### HTTPS证书文件
    
  将iMSDKServer.cer证书文件拖到XCode工程中，并在XCode工程 Build Phases -> Copy Bundle Resources中，确认iMSDKServer.cer文件已经添加到拷贝列表
    
  > 如果没有，可以点击下方“+”，在弹出的选择框中选中添加的证书文件，点击“Add”进行添加
   
  ![XCode Https证书](Images/4_2_unity_setupenv_xcode_cer.jpg)
  *iMSDKServer.cer证书文件获取方法可以参考Android HTTPS配置部分说明*
   
#### 添加资源和插件

**请参考iOS文档进行配置**
    
#### 基础代码调用

Unity编译导出XCode工程后，需要在工程中添加必要的代码，iMSDK插件才能正常运行

* 添加头文件

  在XCode工作中，找到UnityAppController.mm文件，添加头文件引用

  ```mm
  #import <IMSDKCoreKit/IMSDKCoreKit.h>
  ```
* 增加代码调用

  1. 处理应用启动 

    在UnityAppController.mm文件AppDelegate中，找到如下方法

    ```mm
    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(nullable NSDictionary *)launchOptions
    ```

    并在返回前添加如下代码调用

    ```mm
    [[IMSDKApplicationDelegate sharedInstance] application:application
                             didFinishLaunchingWithOptions:launchOptions
                                            withGameSecret:@"YOUR_GAME_SECRET"];
    ```

    > YOUR_GAME_SECRET 为游戏访问iMSDK服务器秘钥串，需要换成真实的秘钥串，可以跟iMSDK后台获取，请[联系我们](../../Pre/contact.md)确认该值

  2. 处理应用拉起

    在UnityAppController.mm文件AppDelegate中，找到如下方法

    ```mm
    - (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(nullable NSString *)sourceApplication annotation:(id)annotation
    ```

    并在返回前添加如下代码调用

    ```mm
    [[IMSDKApplicationDelegate sharedInstance] application:application
                                                        openURL:url
                                              sourceApplication:sourceApplication
                                                     annotation:annotation];
    ```
  
#### 基础信息配置

iOS工程配置主要是修改添加的IMSDKAppSetting.bundle资源文件目录下Contents/Resources/app.plist配置

* Game ID 配置

  在每个游戏接入的时候，都会分配一个游戏ID作为iMSDK应用标识

  在XCode工程中，找到IMSDKAppSetting.bundle/Contents/Resources/app.plist文件，增加或修改如下配置：

  ```xml
  <key>GameId</key>
  <string>11</string>
  ```

  将string值修改为对应的游戏ID

* iMSDK 服务器地址配置

    在XCode工程中，找到IMSDKAppSetting.bundle/Contents/Resources/app.plist文件，增加或修改如下配置：

    ```xml
    <key>IMSDKServer</key>
    <string>sdkapi-beta.itop.qq.com</string>
    ```

    将string值修改为对应的iMSDK服务器地址，不需要添加 “ https:// ”头

* 日志级别配置

    在XCode工程中，找到IMSDKAppSetting.bundle/Contents/Resources/app.plist文件，增加或修改如下配置：

    ```xml
    <key>IMSDKLogLevel</key>
    <integer>1</integer>
    ```
    将integer值修改为对应的日志级别：

    * 1 - Debug
    * 2 - Info
    * 3 - Warn
    * 4 - Error
    * 5 - Assert


* Debug 服务器Host配置[\*]:

    \*一般情况下不需要配置。该配置项主要是用于服务器未配置域名的情况，此时服务器地址可以填写IP，在本配置项中填写服务器地址，如：

    ```xml
    <key>IMSDKServer</key>
    <string>103.7.28.42</string>
    <key>IMSDKServerHost</key>
    <string>sdkapi-beta.itop.qq.com</string>
    ```
 #### 下一步
 
 1. [完成渠道配置](Channel/README.md)
 2. [快速集成](quickstart.md)