---
layout: post
title:  "Push Notifications"
date:   2014-10-02 23:23:23
categories: cocoa
tags: push remote notifications apn android ios cloud
published: true
---

Notifications can contain, a message, a badge, have a sound effect, contain custom json, or just indicate new content.

## iOS

This is the basic App delegate methods you need to implement.

{% highlight objective-c %}

// Register for user notifications
if ([[[UIDevice currentDevice] systemVersion] floatValue] >= 8.0)
  [[UIApplication sharedApplication] registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge) categories:nil]];
else
  [[UIApplication sharedApplication] registerForRemoteNotificationTypes:(UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound)];


// Required app delegate method
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
{
    NSLog(@"deviceToken: %@", deviceToken);
    // Register the device token with a webservice
}

// Required app delegate method
- (void)application:(UIApplication *)application didFailToRegisterForRemoteNotificationsWithError:(NSError *)error
{
    NSLog(@"Error: %@", error);
}

{% endhighlight %}

### iOS 8

iOS8 introduced content only notifications which have taken the place of remote notifications.
Content notifications can be utilised to wake your App (whilst in the background) and check for new content.

First add `remote-notification` to your Info.plist in the `UIBackgroundModes` array.

{% highlight objective-c %}
// Register for content notifications
[[UIApplication sharedApplication] registerForRemoteNotifications];

// New app delegate method
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
{
    // Check with your server if there's new content

    /*
     * Note: you have 30 seconds to do your work and
     * call the completion handler
     */

    UIBackgroundFetchResult result = UIBackgroundFetchResultNoData;
    // You must then call the completion handler
    if(data)
      result = UIBackgroundFetchResultNewData;
    else if(error)
      result = UIBackgroundFetchResultFailed;
    handler(reusult);
}

{% endhighlight %}

The OS will track how long you take in `application:didReceiveRemoteNotification:fetchCompletionHandler:` and Apps which use significant power
may not be woken up for further notifications.


{% if false %}
Standard push notifications are now referred to as User Notifications, and have also have improved capabilities.

Categories


### Server side

Sending
https://github.com/nomad/houston

### Certificates

# Android
{% endif %}
