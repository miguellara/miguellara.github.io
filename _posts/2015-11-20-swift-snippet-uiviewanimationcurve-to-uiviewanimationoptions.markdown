---
layout: post
title: "Swift Snippet: UIViewAnimationCurve to UIViewAnimationOptions"
summary: "Swift function to translate a UIViewAnimationCurve into a UIViewAnimationOptions."
date: 2015-11-19 18:00:00
categories: swift snippet block nstimer
---


{% highlight swift %}
import UIKit

func viewAnimationOptionForCurve(curve: UIViewAnimationCurve) -> UIViewAnimationOptions {
	switch (curve) {
	case .EaseInOut:
		return UIViewAnimationOptions.CurveEaseInOut
	case .EaseIn:
		return UIViewAnimationOptions.CurveEaseIn
	case .EaseOut:
		return UIViewAnimationOptions.CurveEaseOut
	case .Linear:
		return UIViewAnimationOptions.CurveLinear
	}
}
{% endhighlight %}
