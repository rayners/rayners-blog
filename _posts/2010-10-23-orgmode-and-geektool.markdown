--- 
layout: post
title: OrgMode and GeekTool
mt_id: 34
date: 2010-10-23 23:00:00 +01:00
---
I use [OrgMode][orgmode] to manage my task list and I am trying to make it into my main calendar.  One of the things I keep in mind as I work my way through the various configuration options and customizations is that I want to use [OrgMode][orgmode] as little as possible; do what I need to do with it and get back to what I am actually doing.

One of the big problems in that realm that I have run into is that it takes effort for me to view my agenda and to-do list.  Yes, it's a _small_ effort to type `C-c a a` when I'm in emacs, but I still have to remember to do that so I can check it.  Enter [GeekTool][geektool].

With [GeekTool][geektool], among other things, I can stick the output of any shell command onto my desktop.  And [OrgMode][orgmode] has some handy functionality to [extract agenda information](http://orgmode.org/manual/Extracting-agenda-information.html), so I set up a custom agenda to use for [GeekTool][geektool]:

From [`~/.emacs.d/rayners/org.el`](http://github.com/rayners/emacs.d/blob/master/rayners/org.el):

    (setq org-agenda-custom-commands
          '(
            ;; ...
            ("G" "Geektool agenda"
             ((agenda "")
              (alltodo))
             ((org-agenda-ndays 1)
              (org-deadline-warning-days 7))
             ("~/agenda.txt"))
            ))

Which translates to roughly: today's agenda, all my to-do items and warnings for any deadlines in the next week.

<a href="http://rayners.org/assets_c/2010/10/GeekTool-20101024-011514-20.html" onclick="window.open('http://rayners.org/assets_c/2010/10/GeekTool-20101024-011514-20.html','popup','width=624,height=410,scrollbars=no,resizable=no,toolbar=no,directories=no,location=no,menubar=no,status=no,left=0,top=0'); return false"><img src="http://rayners.org/assets_c/2010/10/GeekTool-20101024-011514-thumb-200x131-20.jpg" width="200" height="131" alt="GeekTool-20101024-011514.jpg" class="mt-image-right" style="float: right; margin: 0 0 20px 20px;" /></a>

Next, I added a geeklet in [GeekTool][geektool] that runs the following command: 

    /path/to/emacs --batch \
        -l ~/.emacs.d/init.el \
        -eval '(org-batch-agenda "G")'

 `--batch` nixes the use of my personal emacs customization files, so that's what the `-l ~/.emacs.d/init.el` part is for.

[OrgMode][orgmode] also has a CSV agenda export function that might warrant some exploring in the not too distant future.  If nothing else, it might be a useful link the tool-chain to connect all my various calendars.

  [orgmode]: http://orgmode.org/
  [geektool]: http://projects.tynsoe.org/en/geektool/ 
