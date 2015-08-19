
---
layout: post
title: Swift-er Error Handling 
---

My initial impression of do/try/catch in Swift 2 was that it would only make my code longer and more complex. I was comfortable using optionals and simply checking/ unwrapping them with if/let syntax. Further reading has prompted me to realize that the new error-handling model is better for several reasons:

When you simply check that an optional is non-nil, you aren’t really handling the error. Throwing and catching errors forces you to deal with the errors rather than skip execution.
Do/try/catch allows you to recover. If you catch the errors thrown by the method that you are calling in the do{} block, you’ll be able to recover and tell your user what’s going on.
Writing your error enum (with ErrorType conformance) encourages you to think more intently about the possible error cases during development rather than when bugs start popping up.
-----

