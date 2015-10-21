---
layout: post
title: "Swift Snippet: Small Caps UIFont variant extension"
summary: "Swift snippet that adds an extension to UIFont to produce a Small Caps variant UIFont."
date: 2015-10-21 15:00:00
categories: swift snippet uifont coretext
---


This extension uses CoreText's constants to produce a Small Caps `UIFont` variant by deriving the oritinal font's 
`UIFontDescriptor`.


{% highlight swift %}
extension UIFont {
	
	func smallCapsFontVariant(smallCapsForUppercase: Bool = true) -> UIFont {
		var features = [
			[UIFontFeatureTypeIdentifierKey: kLowerCaseType,
				UIFontFeatureSelectorIdentifierKey: kLowerCaseSmallCapsSelector]
		]
		
		if smallCapsForUppercase {
			features.append([UIFontFeatureTypeIdentifierKey: kUpperCaseType,
				UIFontFeatureSelectorIdentifierKey: kUpperCaseSmallCapsSelector])
		}
		
		let smallCapsFontDescriptor = fontDescriptor().fontDescriptorByAddingAttributes([
			UIFontDescriptorFeatureSettingsAttribute : features
			])
		
		return UIFont(descriptor: smallCapsFontDescriptor, size: 0)
	}
}
{% endhighlight %}
