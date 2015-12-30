---
layout: post
title: Reference Cycles
comments: True
---
Swift is pretty great at managing memory automatically, it uses ARC to allocate memory when it's needed, and free it up when it isn't. I learned more about the *old way* of doing things, before automatic reference counting, and I'm here to tell you that ARC is your friend. 

### So how does ARC work?
The simplest explanation is that ARC automatically allocates memory when you create an instance of a reference type. ARC then keeps track of the number of properties, vars, and lets where you are referencing that instance. This way, ARC will never accidentally deallocate an instance while it's still being used. If it did, when we tried to access the instance, its properties, or its methods, our app would crash. 

### Avoiding strong reference cycles
One of the more complicated matters in memory management is avoiding strong reference cycles between instances. 
When you have two instances that have strong references to each-other, the reference count will never be zero, and ARC will never deallocate them. Here is an example:


{% highlight swift %}

class Minion {
  
    let name: String
    
    init(name: String) {
        self.name = name
    }
    
    var master: Master?
    
    deinit {
        print("\(name) is being deinitialized")
    }
}

class Master {
    
    let name: String
    
    var minion: Minion?
    
    init(name: String) {
        self.name = name
    }
    deinit {
        print("Master \(name) is being deinitialized")
    }

    
}

{% endhighlight %}

Above, I created two classes: Minion and Master. Minion instances will have a name property and an optional Master property. Next, let's create some instances of each class. The two variables are of optional type so that we can later assign them nil values to test if ARC deallocates them. 

{% highlight swift %}
var bob: Minion?
bob = Minion(name: "Bob")

var scarlettOverKill : Master?
scarlettOverKill = Master(name: "Scarlett Overkill")

{% endhighlight %}

Since the Master property is an optional, its default is nil, and likewise for the optional Minion property in Master. Now that we have our instances, we can link them together...

{% highlight swift %}
bob!.master = scarlettOverKill
scarlettOverKill!.minion = bob
{% endhighlight %}

The problem is that now, even if we do the following:

{% highlight swift %}
bob = nil
scarlettOverkill  = nil
{% endhighlight %}

Our deinit messages will never print because both instances still have strong references to each other. 

### How do we fix memory cycles?
Swift addresses the issue above by letting us tell ARC that an instance can refer to another instance without keeping its strong reference. Swift uses the two keywords, "weak" and "unowned."

We use *weak* when it's possible for the reference to become nil at some point. In our example, a minion's master could become nil at some point. 

{% highlight swift %}

class Minion {
...
weak var master: Master?

}
{% endhighlight %}

We use *unowned* when we know that the reference will always have a value. Because of this, when we use 'unowned' our reference can only be of a non-optional type. For argument's sake, let's say that minions will **always have a master.** With this assumption, we could write the following (changing from our example above): 

{% highlight swift %}

class Minion {
...
unowned let master: Master

}

{% endhighlight %}

In either case, if we were to set bob or scarlettOverkill to nil, our deinitialization message will now print out because ARC has deallocated them.



