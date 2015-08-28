---
layout: post
title: Generic Types
comments: True
---

Swift is a fantastic programming language for many reasons. For beginners and experienced programmers alike, Swift offers a lot. As someone new to programming, Swift's syntax is expressive and easy to understand. Experienced programmers will enjoy Swift's modern language features and capabilities. Generics are interesting to me, and I've become more comfortable with them as I've learned more about Swift. 

###About generics
Generics are self-describing. In Swift, generics allow you to write flexible code that avoids redundancy, but retains clarity. As an example, the swap method in the Swift standard library enables you to swap two instances, as long as they are of the same type. This is achieved through generics. 


{% highlight swift %}

var a = 1
var b = 2

swap(&a, &b)
print("a is now \(a) and b is now \(b)")
//prints "a is now 2 and b is now 1"

{% endhighlight %}

Arrays and Dictionaries are, in fact, generic collections. They hold values of any specified type.

###Type parameters
You specify a name for a generic parameter by putting the *placeholder* after the function name, in angle brackets.

{% highlight swift %}

func swapTwoValues<T>(inout a: T, inout _ b: T)

{% endhighlight %}

In the method body, you can use the generic type parameter similarly to a local variable. 
It is common to see these type parameters as <T>. The capitalization will help you remember that these are types and not values.  