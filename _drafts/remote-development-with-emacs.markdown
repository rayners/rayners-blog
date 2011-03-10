---
title: Remote Development with Emacs
---

During the day now, instead of doing my development work locally on my laptop, I write code and tests on a remote server. In a local instance of Emacs. There are some custom tools (on the remote machine) that I use to manage my workflow and development environment, and I have written some elisp to cobble all this together into something mildly useful at times, especially when I combine it with [orgmode][].

Thanks to Emacs' [TRAMP][], it is fairly easy to edit remote files. With a file name in the form of `"/<protocol>:<user>@<host>:<path>"` Emacs will use that protocol to connect to the remote account, make a local copy of the file and push changes to the local file to the remote one.

<aside>

The protocol used is not limited to just remote connections; you can also use `sudo` for example to edit files as though you were running `sudo`.

</aside>

And, as a bonus, when a remote file is opened, features like Emacs' version control that spawn external processes will operate on the remote machine as well. So I can open up a file in a remote directory that is in a git repository and do the version control work I need to do in Emacs itself without having to open a shell on the remote machine at all.

So, for starters, I created a variable to store the remote path where I do the majority of my work.

{% highlight cl %}

    (defvar rayners/remote-dir (format "/ssh:%s@%s:%s" user-login-name rayners/remote-host rayners/remote-project))

{% endhighlight %}

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


  [orgmode]: http://orgmode.org/
  [TRAMP]: http://www.emacswiki.org/cgi-bin/wiki/TrampMode
  
