---
title: No, you shouldn't let it crash
layout: single
---

I recently read a blog post that suggested that software developers should let their software crash once in a while. The author of the post argued that letting software crash was a good thing. He used the following try-catch block to illustrate his point:

try
{
     // stuff
}
catch (SQLException e)
{
     // something went wrong in the database
     // let's fix it
}
catch (Exception e)
{
     // I'm not sure what went wrong
     // but I don't want my application
     // to crash because of it
}

From the blog post:

The intention is good, you want to prevent crashes. And let's face it, crashes are annoying! And can be disastrous for a business; a frequently crashing application will drive away customers. But what do you put in the last catch clause, the one that catches everything that has fallen through? The same thing as you always put in a catch, right? The code to fix the problem. Except you don't know what went wrong.

In my opinion, the author states exactly why you must prevent the crash: a frequently crashing application is bad for business. In an academic setting, it is a good idea to just let software crash. It provides opportunities for students to see problems they may have made in their code, and to correct them. However, the real world isn't about perfect code, it is about working code, under all conditions. Let me explain with an example I've encountered in my career.

I write warehouse control system (WCS) software for a living. Our WCS often interacts with warehouse management system (WMS) software via a messaging protocol. These messages can be sent over a variety of protocols; the details of which are not important to this example. Our software needs to be prepared to receive and process all sorts of data from the WMS. It doesn't matter if the WMS sends us a complete junk message, we need to be able to handle it.

99% of the time we get good data from the WMS. It is formatted correctly, the data makes sense, so we perform the appropriate action based on what was sent to us. However, sometimes we get a bad message that we can't do anything with. The data might be bad or it might not be formatted correctly, or it might literally be junk. Who knows? We don't, and we can't predict all error scenarios. But we need to handle it gracefully, and we need to let the WMS know something was wrong with what was sent.

If we just let it crash when a junk message comes in, we'd log an exception and move on. But when you use the last catch block for that generic exception you didn't expect, you can do smart things. You can give error messages to the user that say "Hey! That didn't make ANY sense." You can send messages back to the host saying that the sent message was junk. Doing these smart things helps everyone from software developers to warehouse operators track down the source of the problem, and solve it.

Letting it crash is useful in the classroom setting. In the real world, we need to handle all problems, expected or not, gracefully. The final catch all for a generic exception lets us do just that.