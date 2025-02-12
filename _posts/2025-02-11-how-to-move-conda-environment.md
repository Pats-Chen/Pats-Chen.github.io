---
layout: post
title:  How to Move Conda Environment
date:   2025-02-11 21:57:00
description: A post on how to move conda environment in Windows
tags: vs-code environment
categories: computer-science
---
Activate the conda environment that you want to move. Then, enter the following command:  

{% highlight Bash linenos %}

conda activate C:\Users\YourUserName\.conda\envs\YourEnvironmentName
conda env export > C:\Users\YourUserName\YourEnvironmentName.yml

{% endhighlight %}

This will create a YAML file that contains the environment's dependencies.  
After that, deactivate the environment, and then remove the environment by the following command:  

{% highlight Bash linenos %}

conda remove --prefix C:\Users\YourUserName\.conda\envs\YourEnvironmentName --all

{% endhighlight %}

Finally, create a new environment by the following command:  

{% highlight Bash linenos %}

conda env create -p E:\ProgramData\Miniconda3\envs\YourNewEnvironmentName -f C:\Users\YourUserName\YourEnvironmentName.yml
del C:\Users\YourUserName\YourEnvironmentName.yml

{% endhighlight %}

Delete the YAML file after creating the new environment. Done!  