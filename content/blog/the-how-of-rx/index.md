---
title: The How of Rx
date: "2019-08-21T19:01:41.393Z"
description: "An introduction into how RxSwift works, from the bottom up."
---

You're a smart iOS developer, and you're particularly fond of reactive programming.
Combine and SwiftUI look very attractive to you.
But you would like to know how it actually works.
Fear not.

We will dive into the very core of RxSwift, starting with the most important type
in all of RxSwift: the **Event**.

The definition of an **event** is simple:

```swift
public protocol Event<Element> {
    case next(Element)
    case error(Error)
    case completed
}
```
