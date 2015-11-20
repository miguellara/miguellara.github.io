---
layout: post
title: "Swift Snippet: NSTimer Block Extension"
summary: "Swift extension to schedule a block in a NSTimer."
date: 2015-11-19 22:00:00
categories: swift snippet block nstimer
---

Schedule a block on a timer using a method similar to the standard SDK.
I think it looks cleaner, and more obvious, when used in the code than the original target-action invocation.

The scheduled block is retained by the `TimerBlock` instance wrapping it, which is in its place retained by the
`NSTimer` scheduler until the timer is fired.


{% highlight swift %}
import Foundation


extension NSTimer {
	
	class func scheduledTimerWithTimeInterval(
		timeInterval: NSTimeInterval, userInfo: AnyObject?, repeats: Bool, block: (timer: NSTimer) -> Void) -> NSTimer
	{
		let minion = TimerBlock(block: block)
		// The `minion` will be retained by the `NSTimer` as its `target`, until the timer is invalidated.
		return NSTimer.scheduledTimerWithTimeInterval(
			timeInterval, target: minion, selector: Selector("timerDidFire:"), userInfo: userInfo, repeats: repeats)
	}
}


final class TimerBlock: NSObject {
	
	private let block: (timer: NSTimer) -> Void
	
	init(block: (timer: NSTimer) -> Void) {
		self.block = block
	}
	
	func timerDidFire(timer: NSTimer) {
		block(timer: timer)
	}
}
{% endhighlight %}
