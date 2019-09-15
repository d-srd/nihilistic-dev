---
title: SwiftUI View State
date: "2019-09-15T12:56:06.316Z"
description: "An overview of the different ways of handling state in Views in SwiftUI"
---

There are five common scenarios when it comes to handling state in views.

## View Property
Read-only access to state
```swift
struct UsernameView: View {
    let username: String
    
    var body: some View {
        Text(username)
    }
}
```

## @State
Observing and updating state local to the View that has a reference to it
```swift
struct UsernameInputView: View {
    @State var username = ""
    
    var body: some View {
        TextField(username, text: $username)
    }
}
```

## @Binding 
Observing and updating state not owned by the View that has a reference to it
```swift
struct UsernameInputView: View {
    @Binding var username: String
    
    var body: some View {
        TextField(username, text: $username)
    }
}
```

## @ObservedObject
Observing state of a reference type object
```swift
struct UserInputView: View {
    @ObservedObject var user: User
    
    var body: some View {
        VStack {
            Text(user.name)
            Text(user.surname)
        }
    }
}
```

## @EnvironmentObject
Observing and updating state that does not belong to any particular View
```swift
struct HighScoreView: View {
    @EnvironmentObject var highScore: HighScore
    
    var body: some View {
        Text(highScore.value)
    }
}
```
