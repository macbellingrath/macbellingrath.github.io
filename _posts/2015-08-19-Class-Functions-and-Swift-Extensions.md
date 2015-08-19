---
layout: post
title: Using Class Functions in Swift Extensions
---


During a recent experimentation with Swift’s extensions, I was reminded about the important distinctions between class and instance methods. I was writing a simple extension of UIColor to save me from retyping the rgb values and converting them to floats. My first attempt looked like this:

{% highlight swift %}

extension UIColor{
func lightRedColor()-> UIColor {
return UIColor(red: 144/255.0, green: 80/255.0, blue: 89/255.0, alpha: 1.0)
}
}

{% endhighlight %}

When I went to declare my color variable, Xcode wouldn’t let me call my new function on UIColor. Instead, I would have had to create an instance using a predefined public class method declared in UIColor and then call my function on that instance.

It might look like this garbage:

{% highlight swift %}
let myColor = UIColor.lightGrayColor().lightRedColor()
{% endhighlight %}

When I looked at the declaration for .lightGrayColor(), I realized that it must be declared as a class function, not as an instance method.

{% highlight swift %}
extension UIColor{
class func lightRedColor()-> UIColor {
return UIColor(red: 144/255.0, green: 80/255.0, blue: 89/255.0, alpha: 1.0)
}
}
{% endhighlight %}

And now, I can call my function on UIColor.

{% highlight swift %}
let myColor = UIColor.lightRedColor()
{% endhighlight %}

It was a simple error, but it served as a good reminder to me to pay attention to when I should be marking my functions with the class keyword.
-----

