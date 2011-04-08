---
title: Revisiting my email usage
tags:
  - email
  - emacs
  - wanderlust
---

I am not good at email. I do not manage email well. I have bad email habits.

# Bad Habits #

If there is a technical topic or software package I have found even remotely interesting at some point in the last decade, I have probably subscribed to a mailing list or two about it. And while I may peruse the incoming list emails from time to time, for the vast majority of them, I do not make a point of reading or at least skimming every email that comes through. 

I also pretend to use Gmail's stars as a to do list. Unfortunately, it's really just an append only list; I don't ever actually reference it, pick a task, do it and then remove it. We all know that is not what email is for, but we do it anyway.

# Potential Solutions #

For the mailing lists, reading them through [gmane](http://gmane.org/) in [gnus](http://www.gnus.org/) looks to be a better way to do it, for how I am reading. It removes the load on my inbox. It allows me to read the lists when I choose to and I do not have to feel bad about not reading emails as they come in (yes, I can auto-archive them with Gmail filters, but I still know they are there).

As for a using email as a task list, that is a bit more complex. The Gmail interface itself is fine, but the key thing I need to start doing is, instead of starring an email when there is a task I need to do, adding the relevant information to a task list of some kind. I am trying to use org-mode to track my to do list, though I have not made much use of it in the last couple months beyond the time tracking features. One of the nice things about org-mode is that a task could potentially contain one or more links to "other things" elsewhere in emacs. Like an email, for example.

# Email in Emacs #

Enter wanderlust. Wanderlust can read IMAP email, org-mode can link to emails in wanderlust.

* Use wanderlust and offlineimap to read my emails locally
   * Fancy and speedy local search software
   * Doing it in emacs allows me to:
     * Use the keyboard controls that I am used to for text editing
     * Integration with org-mode
     * Generally increase potential for automation

