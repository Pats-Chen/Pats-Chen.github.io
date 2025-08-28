---
layout: post
title:  Remove Secrets from Commit History
date:   2025-08-28 14:00:00
description: A post on methods to remove exposed secrets from commit history
tags: git
categories: computer-science
---
Situation:

There is hard-coded secret keys in commit history. The hard-coded string has been removed in files, but the history remains, so it is still exposed.

Goal:

Remove secret keys in commit history

Steps:

Use the following command to install pipx before installing history editing tool on a Macbook. This is used to isolate the environment used by the tool from global environment of the device.

{% highlight Bash linenos %}

brew install pipx

{% endhighlight %}

After that, use the following command to install git-filter-repo. This is used to edit commit history.

{% highlight Bash linenos %}

pipx install git-filter-repo

{% endhighlight %}

Copy a mirror of the current repo and then edit commit history from there. This is used to prevent contaminating the current working environment for other developers.

{% highlight Bash linenos %}

git clone --mirror <YOUR_REMOTE_URL> repo-clean.git
cd repo-clean.git

{% endhighlight %}

Create a file named `replacements.txt` used to replace hard-coded secret keys in commit history. This file should look like the following block.

{% highlight Bash linenos %}

# literal example
literal:OLD_PLAIN_TOKEN_ABC123==>***REMOVED***

# regex example
regex:sk_live_[0-9A-Za-z]+==>***REMOVED***        # Stripe
regex:ghp_[0-9A-Za-z]{36,}==>***REMOVED***        # GitHub PAT
regex:AIza[0-9A-Za-z_-]{35}==>***REMOVED***       # Google API Key
regex:sk-[A-Za-z0-9]{48,}==>***REMOVED***         # OpenAI New Format

{% endhighlight %}

Run the following command to replace secret keys in commit history.

{% highlight Bash linenos %}

git filter-repo --replace-text replacements.txt --refs refs/heads/<YOUR_BRANCH_NAME> --force

{% endhighlight %}

Remove the mirror attribute of the git repo and push changes to a new branch.

{% highlight Bash linenos %}

# set mirror to false
git config remote.origin.mirror false
# push it to a new branch
git push origin refs/heads/<YOUR_BRANCH_NAME>-clean:refs/heads/<YOUR_BRANCH_NAME>-clean

{% endhighlight %}

Push the new branch to the remote origin. Resolve potential conflicts if there are any. Done!  
