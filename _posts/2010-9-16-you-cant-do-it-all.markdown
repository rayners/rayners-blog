--- 
layout: post
title: You Can't Do It All
mt_id: 28
date: 2010-09-16 16:30:00 +01:00
---
This would have gone out to Twitter this morning, had I been able to edit out twenty characters:

> I've come to the conclusion that, whenever there is an option to the number of external items some code should process, the default should never be all of them.

Whether it is an email queue or an arbitrary list of jobs in a [Schwartz](http://search.cpan.org/dist/TheSchwartz/) queue, there are many systems out there that work their way through some list of items; a list they may or may not control themselves.  Under ideal circumstances, the list will be well controlled and kept to a manageable size.  However, users and ideal circumstances are a combination not often seen in nature.

> In theory, there is no difference between theory and practice. But, in practice, there is.

Things happen.  Users misconfigure their software unintentionally (or intentionally?).  Connected systems have bugs.  Entropy exists.  Queues can, and *will*, grow significantly and out of control.

If your software is setup to process the *entire* queue every _X_ minutes, there is absolutely a non-zero percent chance that processing the entire queue will eventually take _X+1_ minutes.  Without any kind of protection against multiple executions, your queue processing processes will begin to pile up until they eat up every resource they can find.  And even with those protections, given a queue of sufficient size, even a single process can bring down a machine.

So, here is what you need to do:

* Expose, via a config option/command line flag/whatever, the maximum number of jobs that can be processed by one instance of your code.
* Make the default value absolutely anything but "all" or "0" or whatever value means "do everything."  Make it a "reasonable" number of items, given what you expect your code to be processing (it could be anywhere from "10000" to "15", depending on the expected jobs).  The key is making it a finite number.  With the setting exposed, users of your software can then tune the queue processing as needed for their own environments (even setting it to "all" if they _really_ want to). 
