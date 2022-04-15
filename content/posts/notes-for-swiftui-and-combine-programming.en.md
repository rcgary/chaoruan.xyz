+++
title = "Notes for SwiftUI and Combine Programming (1)"
date = 2019-11-08T22:54:00+11:00
lastmod = 2022-04-15T15:23:34+10:00
tags = ["swift", "iOS", "swiftUI"]
categories = ["programming"]
draft = false
weight = 2001
+++

I start reading [onevcat](https://onevcat.com/) new book [_SwiftUI and Combine Programming_](https://objccn.io/products/swift-ui) (a great
book to learning SwiftUI if you can read Chinese). I decided to put all the
interest parts and notes in here.

<!--more-->


## First things First {#first-things-first}

We always need to `import` the dependency first

```swift
import SwiftUI
import Combine
```


## Layout all the views in the body {#layout-all-the-views-in-the-body}

```swift
var body: some View {
    /// Layout your view here
}
```

`some View` is a new concept introduced in Swift 5.1, which called [Opaque
Types](https://docs.swift.org/swift-book/LanguageGuide/OpaqueTypes.html). Maybe someday I will write a more detail post for opaque types, in
short, opaque types kind like `protocol` but more powerful.


## Enable Canvas in Xcode {#enable-canvas-in-xcode}

You can preview the UI layouts using _Canvas_, which is convincing by
`PreviewProvider`. As long as your swift file have a `struct` confirm it, you
will able to work with SwiftUI and preview changes using _Canvas_ support (Xcode 11+ and OS X
10.15 + Only)

```swift
struct MyView_Previews: PreviewProvider {
    static var previews: some View {
        MyView()
    }
}
```


### Canvas is not fast {#canvas-is-not-fast}

**At least not fast as I wish**, we still need to build the whole project
first, then it starts working as we hope. But sometimes I found I may
easier break the UI, then Xcode start not happy anymore, showing this on canvas

{{< figure src="images/Blog_ideas/Screen%20Shot%202019-11-07%20at%2010.11.58%20pm_2019-11-07_22-15-44.png" >}}

In this case, we have to **resume** the canvas which **rebuilds** the project again 😢


### Preview with multiple devices {#preview-with-multiple-devices}

Canvas support preview with all devices, so we can work on different size
of screens:

```swift
struct ContentView_Previews : PreviewProvider {
    static var previews: some View {
        Group {
            ContentView()
            ContentView().previewDevice("iPhone SE")
            ContentView().previewDevice("iPad Air 2")
        }
    }
}
```

After some loading 😫, we should see something like this:

{{< figure src="images/Blog_ideas/Screen%20Shot%202019-11-07%20at%2010.26.51%20pm_2019-11-07_22-28-54.png" >}}
