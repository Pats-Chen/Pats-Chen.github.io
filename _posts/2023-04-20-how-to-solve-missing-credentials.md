---
layout: post
title:  How to Solve Missing Credentials
date:   2023-04-20 04:29:00
description: A post on how to setup github credentials for wsl2
tags: vs-code environment
categories: computer-science
---
For Git version < v2.36.1, enter this command:  

{% highlight Bash linenos %}

git config --global credential.helper "/mnt/c/Program\ Files/Git/mingw64/libexec/git-core/git-credential-manager.exe"

{% endhighlight %}

Note that the path should be where Git is installed on your device. After that, the error message listed below should be resolved.  

{% highlight Bash linenos %}

Missing or invalid credentials.
Error: connect EACCES /run/user/1000/vscode-git-431ee25d9d.sock
    at PipeConnectWrap.afterConnect [as oncomplete] (node:net:1157:16) {
  errno: -13,
  code: 'EACCES',
  syscall: 'connect',
  address: '/run/user/1000/vscode-git-431ee25d9d.sock'
}
Missing or invalid credentials.
Error: connect EACCES /run/user/1000/vscode-git-431ee25d9d.sock
    at PipeConnectWrap.afterConnect [as oncomplete] (node:net:1157:16) {
  errno: -13,
  code: 'EACCES',
  syscall: 'connect',
  address: '/run/user/1000/vscode-git-431ee25d9d.sock'
}
/mnt/c/Program\ Files/Git/mingw64/libexec/git-core/git-credential-manager.exe erase: 1: /mnt/c/Program Files/Git/mingw64/libexec/git-core/git-credential-manager.exe: not found
remote: Repository not found.
fatal: Authentication failed for 'github.com/YourOrganization/YourProject.git'

{% endhighlight %}

Reference link: https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-git  