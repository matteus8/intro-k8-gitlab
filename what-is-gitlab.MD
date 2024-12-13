# What is Github and Gitlab
Okay let's admit it. Sometimes the I.T. world is confusing because names are similar and people are proud. But it's still important to know the diffrance between these two terms because they are pretty diffrent at the end of the day.

## What is Github
Github in the most basic terms, is a file/folder platform (website) where you can save stuff. This stuff being scripts, powerpoints, viso diagrams (pretty pictures showing how computers connect), and most importantly A LOT OF CODE.

Github is a free platform designed for CODE! Yes, you can save things I mentioned above, but mostly, it's for code; infrastructure code, readme files (like this one you are reading), python code, ruby code, javascript code, you get the idea.

## What is Gitlab
Gitlab is where pros go to get work done. There is alot to know about gitlab and goes beyond the scope of this blog. But you must know, at a basic level, what we are trying to deploy. As you continue with the deployment, more will be discovered, but in short... Gitlab is essentially github and automation combined.

Think about this as an example. You have a script (powershell or bash) that creates users. Everyday you get an email from your boss asking to create 'user1' or 'user2'. Sometimes your boss asks you to create 10 users in one day. Of course it's not hard to run this script 10 times. But that's not very fun or engaging is it?

So here comes gitlab. Now lets imagine you could set up some automagic, and every time your boss emails you with some criteria, perhaps the title of the email says something or the content of the email has some specific words, a gitlab virtual machine starts and creates the users by running your script. WOW, that would be so cool. Well that is what gitlab can do, and much much more.

## Summary
* Git**hub** is where you save code online for everyone to see.

* Git**lab** is a website/platform that can automagically execute/run this stored code in github.
    * This automagic is done by an event/trigger/pattern that is recognized by gitlab (configured by you the SA). Then a set of instructions, setup by you the SA, are performed on a virtual machine (VM). The VM is started automaticaly and deleted when the intructions are complete. A report of what happened is then provided on the website.

> NOTE: **git** is a command line tool/cli you can install [here](https://git-scm.com/). It helps you work with github/gitlab from the command line rather then the gui/websit. (gui is a graphical user interface)