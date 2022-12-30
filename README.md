# Flurry SDK

[![pod](https://img.shields.io/cocoapods/v/Flurry-iOS-SDK)](https://cocoapods.org/pods/Flurry-iOS-SDK)
[![platform](https://img.shields.io/cocoapods/p/Flurry-iOS-SDK)](https://cocoapods.org/pods/Flurry-iOS-SDK)
[![license](https://img.shields.io/github/license/flurry/flurry-ios-sdk)](https://github.com/flurry/Flurry-iOS-SDK)

## Table of Contents

- [Installation](#installation)
  - [iOS](#ios)
  - [watchOS](#watchos)
  - [tvOS](#tvos)
- [Requirements](#requirements)
- [Examples](#examples)
- [Suppport](#support)
- [License](#license)

## Installation

To install FlurrySDK from CocoaPods, please follow the instructions below. Remember to include `use_frameworks!` if your app target is in Swift.

### iOS

To enable Flurry Analytics:

```ruby
pod 'Flurry-iOS-SDK/FlurrySDK'
```

To enable Flurry Ad serving: 

```ruby
pod 'Flurry-iOS-SDK/FlurrySDK'
pod 'Flurry-iOS-SDK/FlurryAds'
```

To enable Flurry Config:

```ruby
pod 'Flurry-iOS-SDK/FlurryConfig'
```

To enable Flurry Messaging:

```ruby
pod 'Flurry-iOS-SDK/FlurryMessaging'
```

### watchOS

To use FlurrySDK for Apple Watch 2.x Extension:    

```ruby
target 'Your Apple Watch 2.x Extension Target' do 
  platform :watchos, '2.0'
  pod 'Flurry-iOS-SDK/FlurrySDK'
end   
```

### tvOS

To use FlurrySDK for tvOS apps:

```ruby
target 'Your tvOS Application' do
  platform :tvos, '10.0'
  pod 'Flurry-iOS-SDK/FlurrySDK'
end
```

To enable Flurry Messaging for tvOS:

```ruby
pod 'Flurry-iOS-SDK/FlurryMessaging'
```

## Requirements

* iOS 10.0+
* tvOS 10.0+
* watchOS 3.0+

## Examples

Listed below are brief examples of initializing and using Flurry in your project. For detailed instructions, please [check our documentation](https://developer.yahoo.com/flurry/docs/).

### Initialize Flurry

* iOS/tvOS

  To initialize Flurry, please import Flurry in your Application Delegate and start a Flurry session inside `applicationDidFinishLaunching`, as described below.

  ```swift
  func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
      let sb = FlurrySessionBuilder()
            .build(logLevel: FlurryLogLevel.all)
            .build(crashReportingEnabled: true)
            .build(appVersion: "1.0")
            .build(iapReportingEnabled: true)
        
      Flurry.startSession(apiKey: "YOUR_API_KEY", sessionBuilder: sb)
      return true
  }
  ```

* watchOS

  Please follow [our instructions here](https://developer.yahoo.com/flurry/docs/integrateflurry/watchos/).

### Log Events

Use this to log normal events and timed events in your app.

* iOS/tvOS

  ```swift
  // Normal events
  Flurry.log(eventName: "Event", parameters: ["Key": "Value"])
        
  // Timed events
  Flurry.log(eventName: "Event", parameters: ["Key": "Value"], timed: true)
  Flurry.endTimedEvent(eventName: "Event", parameters: ["Key": "Value"])
        
  // Standard events
  let param = FlurryParamBuilder()
      .set(doubleVal: 34.99, param: FlurryParamBuilder.totalAmount())
      .set(booleanVal: true, param: FlurryParamBuilder.success())
      .set(stringVal: "book 1", param: FlurryParamBuilder.itemName())
      .set(stringVal: "This is an awesome book to purchase !!!", key: "note")
        
  Flurry.log(standardEvent: FlurryEvent.purchased, param: param)
  ```
  Please see our [sample project here](https://github.com/flurry/iOS-StandardEventSample).


* watchOS

  ```swift
  FlurryWatch.logWatchEvent("Event", withParameters: ["Key": "Value"])
  ```

### Log Error (iOS/tvOS)

Use this to log exceptions and/or errors that occur in your app. Flurry will report the first 10 errors that occur in each session.

```swift
Flurry.log(errorId: "ERROR_NAME", message: "ERROR_MESSAGE", exception: e)
```

### Track User Demographics (iOS/tvOS)

After identifying the user, use this to log the user’s assigned ID, username, age and gender in your system.

```swift
Flurry.set(userId: "USER_ID")
Flurry.set(age: 20)
Flurry.set(gender: "f") // "f" for female and "m" for male
```

### Session Origins and Attributes (iOS/tvOS)

This allows you to specify session origin and deep link attached to each session, or add a custom parameterized session parameters. You can also add an SDK origin specified by origin name and origin version.

```swift
Flurry.add(sessionOriginName: "SESSION_ORIGIN")
Flurry.add(sessionOriginName: "SESSION_ORIGIN", deepLink: "DEEP_LINK")
Flurry.sessionProperties(["key": "value"])
Flurry.add(originName: "ORIGIN_NAME", originVersion: "ORIGIN_VERSION")
Flurry.add(originName: "ORIGIN_NAME", originVersion: "ORIGIN_VERSION", parameters: ["key": "value"])
```

## Support

* [Flurry Documentation](https://developer.yahoo.com/flurry/docs/)
* [FAQs for Flurry](https://developer.yahoo.com/flurry/docs/faq/)
* [Flurry Support](https://developer.yahoo.com/support/flurry/)

## License

Copyright (c) 2021 Yahoo. All rights reserved.

This project is licensed under the terms of the [Apache 2.0](http://www.apache.org/licenses/LICENSE-2.0) open source license. Please refer to [LICENSE](LICENSE) for the full terms. Your use of Flurry is governed by [Flurry Terms of Service](https://developer.yahoo.com/flurry/legal-privacy/terms-service/).

## Terminologies and Notations
"License" shall mean the terms and conditions for use, reproduction, and distribution as defined by Sections 1 through 9 of this document.

"Licensor" shall mean the copyright owner or entity authorized by the copyright owner that is granting the License.

"Legal Entity" shall mean the union of the acting entity and all other entities that control, are controlled by, or are under common control with that entity. For the purposes of this definition, "control" means (i) the power, direct or indirect, to cause the direction or management of such entity, whether by contract or otherwise, or (ii) ownership of fifty percent (50%) or more of the outstanding shares, or (iii) beneficial ownership of such entity.

"You" (or "Your") shall mean an individual or Legal Entity exercising permissions granted by this License.

"Source" form shall mean the preferred form for making modifications, including but not limited to software source code, documentation source, and configuration files.

"Object" form shall mean any form resulting from mechanical transformation or translation of a Source form, including but not limited to compiled object code, generated documentation, and conversions to other media types.

"Work" shall mean the work of authorship, whether in Source or Object form, made available under the License, as indicated by a copyright notice that is included in or attached to the work (an example is provided in the Appendix below).

"Derivative Works" shall mean any work, whether in Source or Object form, that is based on (or derived from) the Work and for which the editorial revisions, annotations, elaborations, or other modifications represent, as a whole, an original work of authorship. For the purposes of this License, Derivative Works shall not include works that remain separable from, or merely link (or bind by name) to the interfaces of, the Work and Derivative Works thereof.

"Contribution" shall mean any work of authorship, including the original version of the Work and any modifications or additions to that Work or Derivative Works thereof, that is intentionally submitted to Licensor for inclusion in the Work by the copyright owner or by an individual or Legal Entity authorized to submit on behalf of the copyright owner. For the purposes of this definition, "submitted" means any form of electronic, verbal, or written communication sent to the Licensor or its representatives, including but not limited to communication on electronic mailing lists, source code control systems, and issue tracking systems that are managed by, or on behalf of, the Licensor for the purpose of discussing and improving the Work, but excluding communication that is conspicuously marked or otherwise designated in writing by the copyright owner as "Not a Contribution."

"Contributor" shall mean Licensor and any individual or Legal Entity on behalf of whom a Contribution has been received by Licensor and subsequently incorporated within the Work.

