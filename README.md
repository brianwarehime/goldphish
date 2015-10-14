# goldphish
A Maltego transform and machine to identify possible phishing vectors using permutated domains

This is some what of a follow-up to an earlier [blog post](http://nullsecure.org/identifying-phishing-defense-coverage-using-dns/) about analyzing phishing vectors using [dnstwist](https://github.com/elceef/dnstwist). In this post I'll be releasing a new Maltego transform and machine which can quickly and easily analyze a domain and it's permutations to see who owns the domain. 

I'm pretty embarrassed I didn't think to do something like this last time I was analyzing the domains, however, it's two different use-cases, so I don't feel as bad I guess. 

So, the way this works is, you'll open up Maltego and run a machine which will do two things in tandem:

1. Run a modified version of dnstwist which creates a new domain entity for each permutation (i.e. amazoon.com, amaz0n.com)
2. Use a built in transform to look up the name server for that permutated domain. 

The two transforms run hand in hand to build out a map of the infrastructure involved so you can quickly and easily see who owns what domains. Below are two screenshots that show what this will look like.

This screenshot shows the permutated domains for amazon.com as well as the name servers for the domains. You can quickly and easily see the big circle at the top, which shows a connection between a ton of permutated domains and the name servers for amazon.com, which tells us that amazon.com takes a lot of steps to secure other domains (we already covered that in the last blog post).
![http://i.imgur.com/APU5Dy0.png](http://i.imgur.com/APU5Dy0.png)

In this screenshot, I looked at google.com, which is kinda all over the place in terms of name servers. Doesn't look very consistent and is pretty random, unlike Amazon.

![http://i.imgur.com/zlEuQBJ.png](http://i.imgur.com/zlEuQBJ.png)

Another thing we could eventually do with this, is take a bunch of different well known domains and put them all in here, then see if one particular entity is responsible for a lot of different pertmuated domains, for instance, Google owning Amazon.com domains or vice versa.

You can find the transforms and machine for this on my [github](http://www.github.com/brianwarehime/goldphish). All credits for dnstwist go to [https://github.com/elceef](https://github.com/elceef).

## Installation Instructions

To get this up and running, you'll need to do a few things.

1. Download the goldphish.mtz and *.py from my github repo.
2. In Maltego, import the config you just downloaded by going to "Manage" -> "Import Config"
3. Modify the transform by going to "Manage Transforms" and selecting "Goldphish"
4. You'll need to set the Python interpreter to your OS, (i.e. /usr/bin/python) as well as the Working Directory to wherever you saved the Python scripts (i.e. ~/Projects/Goldphish)

![http://i.imgur.com/hqvYW8D.png](http://i.imgur.com/hqvYW8D.png)

## Running the Machine

After the transforms and machine are installed, all you need to do is click on "Machines" in the menubar, then "Run Machine". You'll need to enter whatever domain you are interested in, then it'll start running the machine. Due to the limitations in the community edition, it'll only return so many results per run, so, by using the machine, it'll keep running the same transform every 2 seconds to make sure all the domains show up. 

The machine will keep running until you stop it, so, after you see no more activity for a few runs, you can just click the stop button.

Please let me know if any of the instructions are unclear or if you ran into any issues getting this running.
