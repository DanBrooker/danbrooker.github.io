---
layout: post
title:  "Swift & Objective-C"
date:   2014-10-06 23:23:23
tags: swift obj-c
categories: cocoa
published: true
---

You can include and use CocoaPods in a swift project.

# Objective-C from Swift

To use Objective-C code in swift you need to setup a bridging header to make the Objective-C code visible to Swift.

Add header file to your project (eg. `Bridging-Header.h`). Set the bridging header in the `Build Setings` (eg. `YourApp/BridgingHeader.h`).
Then add `#include`s into the bridging header.

{% highlight objective-c %}
#import <AFNetworking/AFNetworking.h>
{% endhighlight %}

# Swift from Objective-C

XCode generates a header for you to include, named after your project  `ProjectName-Swift.h`

If a swift class doesn't subclass an Objective-C object then the Swift class needs to be marked `@objc`

{% highlight swift %}
@objc class YourObject {
  // ...
}
{% endhighlight %}

# Further

More from [Apple][apple-swift]

[apple-swift]: https://developer.apple.com/library/ios/documentation/Swift/Conceptual/BuildingCocoaApps/MixandMatch.html
