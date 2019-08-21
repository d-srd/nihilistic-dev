---
title: The How of Rx
date: "2019-08-21T19:01:41.393Z"
description: "An introduction into how RxSwift works, from the bottom up."
---

You're a smart iOS developer who's particularly fond of reactive programming.
Combine and SwiftUI look very attractive to you.
But you would like to know how it actually _works_.

Fear not, young padawan.

We will dive into the very essence of RxSwift, 
continuing to build our knowledge on the foundations
laid out before us by the elders.

The holy trinity of RxSwift is:
- Event
- Observer
- Observable

### The Event

The definition of an **event** is simple:

```swift
public enum Event<Element> {
    case next(Element)
    case error(Error)
    case completed
}
```
