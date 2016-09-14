---
layout: post
title:  "Internet Security"
date:   
categories:
---
Here there is a few images I would like to show on my site: https://www.andrewmunsell.com/blog/passwords/

I have been very very wary of open source for a long time. But I finally pushed some of the stuff I have been playing around with to Github over the weekend.

In about less than a minute, I got an email, see below:

> Subject: Warning: Your Azure storage account (xxxxblob) might be exposed
> Hi there!
> Your Azure storage credentials are publicly visible from GitHub:
> - Storage account: xxxxblob
> - Storage key: jaa1NNN...

After reading that email, shivers went down my spine, and then I realised, even more of my personal information have been compromised. I had a database connection string password that also happened to be a password that followed a pattern I use on other internet accounts, including Paypal and my bank.

Immediately, I started changing all of my passwords, and disabled all of my Azure services, and took a step back to think about the consequences, and any other potential vulnerabilities. I decided to leave the repository as it was on Github, because once something gets on the internet, there’s no going back.

I came up with a new, stronger and secure password pattern, and again started changing all of my paswords (well the ones that mattered to me) again.

When I got to paypal, I hit this screen….

https://xkcd.com/936/
