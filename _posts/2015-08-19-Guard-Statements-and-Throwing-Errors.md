---
layout: post
title: Guard Statements and Throwing Errors
---

* Today, I learned more about using the guard statement and how to throw and catch errors. In my playground, I have written a function to make some cookies. The function accepts one argument, an array of type string. By marking my function with the ‘throws’ keyword, I am telling the compiler that my function is capable of throwing errors. When calling this function, one will be required ( by the compiler ) to call within a ‘do’ block, and must “try” and “catch”, appropriately. 
Guard is a lot like ‘if’ in swift, except that it is always followed by an ‘else’ clause. The guard statement is evaluated, and if false, executes the code inside the ‘else’ clause. You can have many guard statements after another, but after your code evaluates a guard statement to be false, it will execute the else clause and skip to the end of the function. 
I begin by declaring a variable named ‘pantry,’ initialized with an array of the ingredients in my pantry. I then try my ‘makeCookies’ function, passing in the pantry array. You can see that the function is throwing cookieErrors.NotEnoughButter. Because the error was caught, the playground prints out “You’re gonna need some butter.”
I’m excited to learn more about error handling, and how I can improve the readability and intent of my code.
-----

