---
layout: post
title:  How to Check Port Used
date:   2025-03-16 21:52:00
description: A post on methods to check port used in Windows
tags: windows port
categories: computer-science
---
Start a Windows Terminal window and enter the following command:  

{% highlight Bash linenos %}

netstat -ano | findstr LISTENING

{% endhighlight %}

This will use ```netstat``` to list all the ports that are currently in use.
The output will be like this:  

{% highlight Bash linenos %}

  TCP    0.0.0.0:135            0.0.0.0:0              LISTENING       1728
  TCP    [::]:445               [::]:0                 LISTENING       4

{% endhighlight %}

Make sure that the port is not being used by another application if you want your application to run on that port. Done!  