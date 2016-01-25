---
layout: post
title: Building a server with Swift
comments: True
---
It is cool to see that programmers are excited about using Swift to build for uses and platforms beyond Apple. There are several web frameworks written in Swift, but the most elegant that I have seen so far is [Vapor](https://github.com/tannernelson/vapor). 

#####From the repo:
> "A Laravel/Lumen Inspired Web Framework for Swift that works on iOS, OS X, and Ubuntu."

In order to use it, you'll need Swift 2.2. You can get it [here]("https://swift.org/builds/xcode/swift-2.2-SNAPSHOT-2016-01-11-a/swift-2.2-SNAPSHOT-2016-01-11-a-osx.pkg").
The installer will install an Xcode toolchain, which includes the resources you need to work with a particular version of Swift. To use the toolchain from the command-line, I had to add it to my Path.
> $ export PATH=/Library/Developer/Toolchains/swift-latest.xctoolchain/usr/bin:"${PATH}"

I chose to use the [Swift Package Manager](https://github.com/apple/swift-package-manager) for dependency management. 

#### Now, the fun stuff. 

Create an empty directory and name it whatever you like. Then create a file named "Package.swift". The SPM uses this manifest file to fetch and build any dependencies.  The syntax for my Package.swift file is:
{% highlight swift %}

import PackageDescription

let package = Package(
	name: "server",
    dependencies: [
        .Package(url: "https://github.com/tannernelson/vapor.git", majorVersion: 1),
    ])
{% endhighlight %}

Then, run **$ swift build**. You should see it fetch the dependency and build it in the directory you just created.

>Cloning https://github.com/tannernelson/vapor.git
Using version 1.0.5 of package vapor
Compiling Swift Module 'Vapor' (12 sources)
Linking Library:  .build/debug/Vapor.a
Compiling Swift Module 'server' (1 sources)
Linking Executable:  .build/debug/server

In your project directory, create a file named main.swift, and we'll import our module.
{% highlight swift %}
import Vapor
import Foundation
{% endhighlight %}

Vapor's syntax is simple. We create our server by initializing an instance of Server, and call .run() to start it. You may also pass .run() an argument for the port that you want to run your server on.

{% highlight swift %}
let server = Server()
server.run(port: 8080)

{% endhighlight %}


You can specify routes. To respond with JSON, create a dictionary to return from your Route.
{% highlight swift %}
Route.get("date") { request in
    return ["date" : String(NSDate()) ]
}
{% endhighlight %}

This returns:
>{ "greeting": "2016-01-25 14:26:22 +0000" }

In order to test the server out, run **$ swift build**. An executable will be put in *.build/debug/server* . Run the executable from there, and make sure that your ports are open. Navigate to the port that you specified when you created your server (ie: localhost: 8080) and a route that you created in your swift file ("/date"). Voila, a simple server, written in Swift!


Vapor also supports views and controllers, and it looks like they are working on implementing resource controllers. I'm excited to see how the community continues to embrace Swift and demonstrate all of its possibilities. 