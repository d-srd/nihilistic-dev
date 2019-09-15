---
title: Swift for Experienced Developers
date: "2019-08-31T07:10:28.643Z"
description: "TL;DR Swift!"
---

## The Basics
Swift is an expressive, type-safe, high-performance programming language 
enabling functional, object oriented, and procedural programming.

It was initially started by Chris Lattner in 2010, growing in size 
and support as the years went by. WWDC 2014 introduced Swift to the
public, and it was open sourced in 2015. Lattner describes its goal
as [world domination](https://atp.fm/205-chris-lattner-interview-transcript) 
(section 'Swift and Tesla').

### Variables and non-variables
We can alter variables:
```swift
var pizzaCount = 6

pizzaCount = 5 		// whoops ate one
```

But not constants:
```swift
let euler = 2.718
euler = 3 			// compiler error
```

This holds for references (more on those later) as well:
```swift
class Pizza { 
	let slices: Int 
	
	init(slices: Int) { self.slices = slices }
}

var margherita = Pizza(slices: 6)
margherita = Pizza(slices: 2) 		// don't write blogs when you're hungry

margherita.slices = 0 				// compiler error, cannot mutate a constant
```
What's happening here is that we have a reference to an instance of a class.
If it's mutable, we can reassign that reference to any other instance of the same class.
However, any non-mutable properties of that class cannot be changed. Makes sense.

Let's reverse the roles.
```swift
class Pizza {
	var slices: Int

	init(slices: Int) { self.slices = slices }
}

let capricciosa = Pizza(slices: 6)
capricciosa.slices = 2				// perfectly fine - the property is mutable

capricciosa = Pizza(slices: 0) 		// compiler error, cannot reassign reference
```

## Square pegs in round holes
Swift is a type-safe language. Meaning 

## The Memory Model
Swift uses a form of garbage collection called [automatic reference counting](https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html)
for memory management. 


```swift
```
