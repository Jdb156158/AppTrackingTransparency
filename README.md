# AppTrackingTransparency
iOS 14 Checklist-App Tracking Transparency（ATT）适用于请求用户授权，访问与应用相关的数据以跟踪用户或设备

# 用户授权效果图

<img src="./READMEIMAGE/Simulator Screen Shot - iPhone 8 - 2020-12-23 at 13.28.49.png" style="zoom:25%;" />

<img src="./READMEIMAGE/Simulator Screen Shot - iPhone 8 - 2020-12-23 at 14.06.08.png" style="zoom:25%;" />


# 注意事项：
*  App Tracking Transparency（ATT）适用于请求用户授权，访问与应用相关的数据以跟踪用户或设备。 访问 https://developer.apple.com/documentation/apptrackingtransparency了解更多信息。
*  SKAdNetwork（SKAN）是 Apple 的归因解决方案，可帮助广告客户在保持用户隐私的同时衡量广告活动。 使用 Apple 的 SKAdNetwork 后，即使 IDFA 不可用，广告网络也可以正确获得应用安装的归因结果。 访问 https://developer.apple.com/documentation/storekit/skadnetwork 了解更多信息。
苹果未要求开发者配置之前，开发者请勿配置ATT，当前阶段配置后会影响idfa 的获取，从而影响广告收益。
# Checklist
* 应用编译环境升级至 Xcode 12.0 及以上版本

* 如果集成了第三方广告SDK，需求其提供了 iOS 14 与 SKAdNetwork 支持

* 将第三方广告SDK的 SKAdNetwork ID 添加到 info.plist 中，以保证 SKAdNetwork 的正确运行

	```xml
	<key>SKAdNetworkItems</key>
  <array>
    <dict>
      <key>SKAdNetworkIdentifier</key>
      <string>238da6jt44.skadnetwork</string>
    </dict>
    <dict>
      <key>SKAdNetworkIdentifier</key>
      <string>22mmun2rn5.skadnetwork</string>
    </dict>
  </array>
  ```
  
* 支持苹果 ATT：从 iOS 14 开始，若开发者设置 App Tracking Transparency 向用户申请跟踪授权，在用户授权之前IDFA 将不可用。 如果用户拒绝此请求，应用获取到的 IDFA 将自动清零，可能会导致您的广告收入的降低
  要获取 App Tracking Transparency 权限，请更新您的 Info.plist，添加 NSUserTrackingUsageDescription 字段和自定义文案描述。代码示例：
	```xml
<key>NSUserTrackingUsageDescription</key>
<string>该标识符将用于向您投放个性化广告</string>
  ```

# Swift 代码示例
```swift
import AppTrackingTransparency
import AdSupport
func requestIDFA() {
  ATTrackingManager.requestTrackingAuthorization(completionHandler: { 	status in
    // Tracking authorization completed. Start loading ads here.
    // loadAd()
  })
}
```


# Objective-C 代码示例
```objective-c
#import <AppTrackingTransparency/AppTrackingTransparency.h>
#import <AdSupport/AdSupport.h>
- (void)requestIDFA {
  [ATTrackingManager 		requestTrackingAuthorizationWithCompletionHandler:^(ATTrackingManagerAuth	orizationStatus status) {
    // Tracking authorization completed. Start loading ads here.
    // [self loadAd];
  }];
}
```
