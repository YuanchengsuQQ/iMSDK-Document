## 4.2.1 Android 环境配置

### 配置基础信息

  Android工程配置主要是修改Assets/Plugins/AndroidManifest.xml文件

  * Game ID 配置

    在每个游戏接入的时候，都会分配一个游戏ID作为iMSDK应用标识

    在AndroidManifest.xml中找到配置项：

    ```xml
    <meta-data android:name="com.tencent.imsdk.GameId" android:value="\ 11"/>
    ```

    将value值修改为对应的游戏ID。注意，前面的"\\"和空格须保留

  * Keystore SHA1指纹配置
  
    iMSDK 会通过应用的签名信息进行App的身份验证，请在向iMSDK申请游戏应用时，提供正确的SHA1值，或者[联系我们](../../Pre/contact.md)进行确认！

  * iMSDK 服务器地址配置

    在AndroidManifest.xml中找到配置项：

    ```xml
    <meta-data android:name="com.tencent.imsdk.SdkServer" android:value="sdkapi-beta.itop.qq.com"/>
    ```

    将value值修改为对应的iMSDK服务器地址，不需要添加 “ https:// ”头

  * 日志级别配置

    在AndroidManifest.xml中找到配置项：

    ```xml
    <meta-data android:name="com.tencent.imsdk.debug.level" android:value="2" />
    ```
    将value值修改为对应的日志级别：

    * 2 - Vibose
    * 3 - Debug
    * 4 - Info
    * 5 - Warn
    * 6 - Error
    * 7 - Assert


  * Debug 服务器Host配置[\*]:

    \*一般情况下不需要配置。该配置项主要是用于服务器未配置域名的情况，此时服务器地址可以填写IP，在本配置项中填写服务器地址，如：

    ```xml
    <meta-data android:name="com.tencent.imsdk.DebugServerHost" android:value="sdkapi-beta.itop.qq.com"/>
    <meta-data android:name="com.tencent.imsdk.SdkServer" android:value="103.7.28.42"/>
      ```

#### 下一步

1. [完成渠道配置](Channel/README.md)
2. [快速集成](quickstart.md)