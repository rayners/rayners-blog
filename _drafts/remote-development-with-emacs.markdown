---
title: Remote Development with Emacs
---

During the day now, instead of doing my development work locally on my laptop, I write code and tests on a remote server. In a local instance of Emacs.

{% highlight cl %}

    (defvar rayners/remote-dir (format "/ssh:%s@%s:%s" user-login-name rayners/remote-host rayners/remote-project))
    (defun rayners/dev-connect ()
      "Make sure we've setup a connection to the remote host"
      (interactive)
      (tramp-maybe-open-connection (tramp-dissect-file-name rayners/remote-dir))
    
    (defmacro with-remote-dir (&rest body)
      (rayners/dev-connect)
      `(let ((default-directory rayners/remote-dir))
        (progn ,@body)))

{% endhighlight %}
