---
title: Remote Development with Emacs
---

During the day now, instead of doing my development work locally on my laptop, I write code and tests on a remote server. In a local instance of Emacs. There are some custom tools (on the remote machine) that I use to manage my workflow and development environment, and I have written some elisp to cobble all this together into something mildly useful at times, especially when I combine it with [orgmode][].

Thanks to Emacs' [TRAMP][], it is fairly easy to edit remote files. With a file name in the form of `"/<protocol>:<user>@<host>:<path>"` Emacs will use that protocol to connect to the remote account, make a local copy of the file and push changes to the local file to the remote one.

<aside>
The protocol used is not limited to just remote connections; you can also use `sudo`, for example, to edit files as though you were running `sudo`.
</aside>

And, as a bonus, when a remote file is opened, features like Emacs' version control that spawn external processes will operate on the remote machine as well. So I can open up a file in a remote directory that is in a git repository and do the version control work I need to do within Emacs itself and without having to open a shell on the remote machine.

So, for starters, I created a variable to store the remote path where I do the majority of my work.

{% highlight cl %}

    (defvar rayners/remote-dir (format "/ssh:%s@%s:%s" user-login-name rayners/remote-host rayners/remote-project))

{% endhighlight %}

Next, I created a function that would make sure the proper initialization steps were taken with the connection and a macro that I could use to evaluate elisp code in the context of the remote machine.

{% highlight cl %}

    (defun rayners/dev-connect ()
      "Make sure we've setup a connection to the remote host"
      (interactive)
      (tramp-maybe-open-connection (tramp-dissect-file-name rayners/remote-dir))
    
    (defmacro with-remote-dir (&rest body)
      (rayners/dev-connect)
      `(let ((default-directory rayners/remote-dir))
        (progn ,@body)))

{% endhighlight %}

And then some elisp to a) get a list of colleagues to whom I could submit a patch for review and b) perform the actual patch submit.

{% highlight cl %}

    (defvar rayners/tool-submit-hooks nil "hook variable for patches that are being submitted")

    (defun rayners/submitters ()
      (interactive)
      (with-remote-dir
        (with-temp-buffer
          (shell-command "shell_command_to_get_colleague_list" t)
          (split-string (buffer-string)))))
    
    (require 'ido)
    (defun rayners/gitc-submit ()
      (interactive)
      (let ((submitters (rayners/submitters)))
        (let ((submit-to (ido-completing-read "Submit to: " submitters)))
          (with-remote-dir
           (shell-command (format "submit_tool %s &" submit-to) "*submit_tool*"))
          (run-hooks 'rayners/tool-submit-hooks))))

{$ endhighlight %}

Notice the hook there? I use [orgmode][] to track my time, and I thought it would be super-nifty if I could automatically stop the clock for the current task when I submit a patch.

{% highlight cl %}

    (defun rayners/submit-clock-out ()
      "Clock out when submitting, unless arg is present"
      ;; clock out of the current task timer
      ;; unless there was a prefix argument
      (if (org-clock-is-active)
          (org-clock-out)))
    (add-hook 'gitc-submit-hooks 'rayners/submit-clock-out)

{% endhighlight %}

  [orgmode]: http://orgmode.org/
  [TRAMP]: http://www.emacswiki.org/cgi-bin/wiki/TrampMode
  
