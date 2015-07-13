---
layout: post
title:  "Where's my KVO?"
summary: "Swift class properties that post KVO notifications."
date:   2015-07-11 22:00:00
categories: swift workaround snippet kvo
---

I love my **KVO** ([Key-Value Observing](http://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/KeyValueObserving/)) and I have used it like crazy in the past in Objective-C, lately through [ReactiveCocoa](https://github.com/ReactiveCocoa/ReactiveCocoa). And it was the first thing that I missed when I started working with Swift.

One solution is to mark your class with `@objc`. `NSObject` is no longer works it magic behind pure Swift classes, and Swift attributes/properties no longer take part on Key-Value coding. In Objective-C you could rely on synthesized `@property`'s or even override `+ (NSSet<NSString *> *)keyPathsForValuesAffectingValueForKey:(NSString *)key`.

The best solution I have for now, to keep classes purely in Swift, is the following snippet. Use it as a template to make Swift properties that generate KVO notifications when properties are set.

{% highlight swift %}
class MyClass: NSObject {
	
	// Private variable not to be KVO observed.
	private var _foo = HyperionAuthenticationStep.Credentials
	
	// Public variable to be KVO observed.
	var foo: SomeType {
		get {
			return _foo
		}
		set(newValue) {
			willChangeValueForKey("foo")
			_foo = newValue
			didChangeValueForKey("foo")
		}
	}
}
{% endhighlight %}

Admittedly, there is a lot of repetition, and I hate the `"foo"` strings lying around, but I still haven't found a good way of using preprocessor macros or reflection in Swift. I'm sure it will come around... eventually!