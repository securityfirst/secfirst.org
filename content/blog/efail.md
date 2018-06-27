---
title: "Efail"
date: 2018-05-15
---

**Efail**
=====================================

![image](efail.jpg)

*This post was created for the "Email" lesson of Umbrella, the free, open-source security advice app for people at risk. Get Umbrella from [Google Play](https://play.google.com/store/apps/details?id=org.secfirst.umbrella), [Amazon](https://www.amazon.com/Security-First-Umbrella-made-easy/dp/B01AKN9M1Y), and [F-Droid](https://secfirst.org/fdroid/repo/?fingerprint=39EB57052F8D684514176819D1645F6A0A7BD943DBC31AB101949006AC0BC228).*

This week, security researchers released information about vulnerabilities in PGP email clients that could expose past or future content, even if it was encrypted. EFF [warned] (https://www.eff.org/deeplinks/2018/05/not-so-pretty-what-you-need-know-about-e-fail-and-pgp-flaw-0) users of these email clients to disable or uninstall PGP plugins and switch to another secure communication method. The list of email clients includes Thunderbird with Enigmail, which are recommended in Umbrella PGP tool guides.   

Here's what you need to know: 

* Secure messaging services like Signal are easier, more common, and therefore more reliable, than encrypting email. So this is good advice. If you're sending sensitive information, do it in a secure message instead of an email. (Learn more about Umbrella's "Sending a Message" lesson.)

* EFF suggests disabling PGP email clients to prevent them automatically decrypting messages, which *could* make the content vulnerable. This is also good advice, but as EFF says, it is "a temporary, conservative" stopgap. It does *not* mean that PGP encryption is insecure, or that you should send unencrypted email.  

* As in all security scenarios, consider your personal threat model. (Learn more about this in Umbrella's "Managing Information" chapter.) If you are at high risk of sophisticated, targeted attacks on encrypted email content, a conservative stopgap will be appropriate. If your risk is low, it may not be. 

If you choose to continue using email, encrypting it using PGP is still much better than not encrypting it at all. But do the following:         

1. Make sure all the software you are running is up to date. Install new updates *immediately*. (You'll be doing this anyway if you've read Umbrella's "Malware" lesson.)

2. Check the [settings] (https://twitter.com/GPGTools/status/995986721891405825?s=19) in your email client for an option to "Load remote content in messages." This option should be disabled or *unchecked*. That's because the attack assumes a hacker can already access your encrypted email, and change the HTML code that pulls in some content, like images, from a remote server. That change could let them see the entire email without encryption if the email client has not implemented the right update yet. 

3.  Follow Efail developments carefully. We'll be posting updates on Twitter [@_SecurityFirst] (https://twitter.com/_SecurityFirst).
