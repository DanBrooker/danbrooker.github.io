---
layout: post
title:  "App Extensions"
date:   2015-03-09 09:55:23
tags: ios app extension today widget share
categories: Cocoa
published: true
---

I created two iOS App extension for my App [Take Note][Take Note]

# Share Extension

A share extension is a separate process to your App

{% highlight swift %}
// Example showing an App that accepts `Text` and `URL`
override func didSelectPost() {
  if let item = extensionContext?.inputItems[0] as? NSExtensionItem {

  //            println("extension item \(item)")
      if let attachments = item.attachments as? [NSItemProvider] {

          var validAttachments = attachments.filter({ $0.hasItemConformingToTypeIdentifier("public.url") || $0.hasItemConformingToTypeIdentifier("public.plain-text")  })
          for (i, provider: NSItemProvider) in enumerate(validAttachments) {

              if provider.hasItemConformingToTypeIdentifier("public.url") {

                  provider.loadItemForTypeIdentifier("public.url", options: nil) { decoder, error in
                      if let url = decoder as? NSURL {
                          text = "\(text) - \(url.absoluteString!)"
                      }

                      if i+1 == validAttachments.count {
                          self.send(text)
                      }
                  }

              } else if provider.hasItemConformingToTypeIdentifier("public.plain-text") {
                  provider.loadItemForTypeIdentifier("public.plain-text", options: nil) { decoder, error in
                      if let string = decoder as? String {

                          if self.contentText != string {
                              text = "\(text) - \(string)"
                          }
                      }

                      if i+1 == validAttachments.count {
                          self.send(text)
                      }
                  }
              }
          }

      }
  } else {
      send(text)
  }
}

func send(text: String) {
    // Write `text` into shared container here

    // Complete extension transaction
    self.extensionContext!.completeRequestReturningItems([], completionHandler: nil)
}

{% endhighlight %}

# Today Widget

A today widget needs to display some useful information to a user and will probably also open the App with context on tap.

Because you probably can't just read your Apps data store, your App will need to write to a shared container which can be read by a today widget.

{% highlight swift %}
// Open App with custom URL scheme
if let url = NSURL(string: "take-notes://text") {
    self.extensionContext?.openURL(url, completionHandler:nil)
}
{% endhighlight %}

[Take Note]: http://take-note.io/
