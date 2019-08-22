---
title: The What of Rx
date: "2019-08-21T19:01:41.393Z"
description: "An introductory tour of the inner workings of RxSwift, from the bottom up."
---

You're a smart iOS developer who's particularly fond of reactive programming.
Combine and SwiftUI look very attractive to you.
But you would like to know how it actually _works_.

Fear not, young padawan.

We will dive into the very essence of RxSwift, 
continuing to build our knowledge on the foundations
laid out before us by the elders.

The holy trinity of RxSwift consists of:
- Event
- Observer
- Observable

### The Event

The definition of an event is simple:

```swift
public enum Event<Element> {
    case next(Element)
    case error(Error)
    case completed
}
```

Its impact is anything but.

We can now model anything. 

Want to see a slightly exaggarated history of the entire universe?

```swift
struct History {
    // TODO: take general relativity into consideration
    let timestamp: Int
    let description: String
}

let entireUniverse: [Event<History>] = [
    .next(History(timestamp: -1, description: "...")),
    .next(History(timestamp: 0, description: "boom")),
    .next(History(timestamp: (14 - 5) * 3e19, description: "Formation of Earth")),
    .next(History(timestamp: (14 - 13) * 3e19, description: "Dinosaurs also boom"),
    .next(History(timestamp: (14 - 13) * 3e19, description: "Facebook facing fines in EU"))
]
```

Want to see some real word network responses?

```swift
let realWorldNetworkResponses: [Event<(HTTPURLResponse, Data)>] = [
    .next((.success, "{\"Hello\": \"World\"}".data(using: .utf8)!)),
    .error(ResponseError(statusCode: 500, message: "Internal server error"))
    .next((.success, "{\"Hello\": \"You\"}".data(using: .utf8)!)),
]
```

You get the picture. 

As Rule 34, addendum 21 states:
> If it exists, there is an RxSwift representation of it.

But what would be even more useful than an array of events would be a way to push
those events somewhere and subscribe to them somewhere else.
That would allow us to combine events together, wait until all three of our mandatory
events complete, create new events out of thin air, filter only for events matching
a desired predicate, or something else entirely.

We're getting a bit ahead of ourselves, so let's slow down and smell the observers.


### The Observer

It has a very simple definition as well:

```swift
public protocol ObserverType {
    associatedtype Element

    func on(_ event: Event<Element>)
}
```

> Side note: I've always found the RxSwift way of naming things confusing. Still do.
> The Combine framework is much clearer in this regard:
> events are pushed into a `Subscriber`, and they are published from a `Publisher`.
> Easy peasy.

An `Observer` is a thing that does something when an event comes.
Let's implement a crude version of an `Observer`, storing all events
in some backing storage until we need to access them.

```swift
public class Observer<Element>: ObserverType {
    private let queue: DispatchQueue = .init(label: "thread-safe-array", attributes: .concurrent)
    private var events: [Event<Element>] = []
    
    public func on(_ event: Event<Element>) {
        queue.async(flags: .barrier) {
            self.events.append(event)
        }
    }
}
```

We can now put our events into a box in order to retrieve them later. 
And hopefully do something with them.

```swift
struct Animal {
    let identifier: String
    
    init(_ identifier: String) {
        self.identifier = identifier
    }
}

let dog = Animal("🐶")
let fox = Animal("🦊")
let penguin = Animal("🐧")
let currentBackyardResident = Observer<Animal>()
currentBackyardResident.on(.next(dog))
currentBackyardResident.on(.next(fox))
currentBackyardResident.on(.next(penguin))
currentBackyardResident.on(.completed)
```
