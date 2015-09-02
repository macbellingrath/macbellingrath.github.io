---
layout: post
title: Type Properties
comments: True
description: In addition to instance properties, structs, enums, and classes can also have type properties. The difference is that instance properties belong to an instance, and type properties belong to the type. 
---
In addition to instance properties, structs, enums, and classes can also have type properties. The difference is that instance properties belong to an instance, and type properties belong to the type. For example, if we had a struct ‘Fruit’ and declared a stored instance property variable ‘name,’ every time that we created an instance of that struct, it would have its own unique value for that property. 

{% highlight swift %}

struct Fruit {
    
    var name: String!
    
}
{% endhighlight %}

So we could create an instance of Fruit and assign it the name of “banana”. 

{% highlight swift %}
let banana = Fruit(name: "banana")
{% endhighlight %}

So we have our banana, but what if we wanted to give our Fruit struct a property that applied to _all_ fruit? This is where **type** properties come in. Type properties do not belong to each instance of the type, but to the type itself. This means that there is only one copy of a specific type property, regardless of how many instances of the type that we have. Let’s say that we want to declare a constant that would apply to all fruit, perhaps the recommended servings per day:

{% highlight swift %}
struct Fruit {    
    static let recommendedServingsPerDay = 9
    var name: String!
}
{% endhighlight %}

Notice the use of the keyword **Static** at the beginning of the declaration. This indicates that this constant belongs to our Fruit type, not to individual instances of Fruit. If I were to type something like: 

{% highlight swift %}
print(banana.reommendedServingsPerDay)
{% endhighlight %}

The compiler will tell you that Fruit does not have a member named recommendedServingsPerDay, and this is true because recommendedServingsPerDay belongs to our _type_. 

Note that stored type properties must be given a default value, unlike stored instance properties.
