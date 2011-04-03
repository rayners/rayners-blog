---
title: Retooling
---

While I am still continuing to use emacs, I am taking some time to try out new some new tools.

* [jabber.el](http://emacs-jabber.sourceforge.net/) instead of [Adium](http://adium.im/)
* [wanderlust](http://www.gohome.org/wl/) instead of Gmail's web interface (and possibly replacing [Thunderbird](http://www.mozillamessaging.com/en-US/thunderbird/) too)
 * With [offlineimap](http://offlineimap.org/) and [imapfilter](https://github.com/lefcha/imapfilter) to go with it, but I am still getting those setup
 
I'm also doing alot of poking around with elisp and [org-mode](http://orgmode.org) to streamline my workflow, and giving the [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) zsh framework a go.

Oh, and I have switched to [jekyll](http://jekyllrb.com/) for my blog, with [Disqus](http://disqus.com/) handling the commenting. The blog is currently stored in a git repository on rayners.org (whose registrar I just switched from GoDaddy to [Namecheap](http://www.namecheap.com?aff=17535)) and is published automatically with a post-receive hook whenever I push to that repository. Now I can even blog in emacs!

For the curious, here are the contents of that hook:

    #!/bin/bash
    
    GIT_REPO=$HOME/git/rayners-blog.git
    TMP_GIT_CLONE=$HOME/tmp/rayners-blog
    PUBLIC_WWW=/var/www/domains/www.rayners.org/jekyll
    
    . $HOME/.rvm/scripts/rvm
    
    git clone $GIT_REPO $TMP_GIT_CLONE
    jekyll --no-auto $TMP_GIT_CLONE $PUBLIC_WWW
    rm -Rf $TMP_GIT_CLONE
    exit

And I am completely redoing the blog's design and layout and such. I cannot promise it is any good, but at least it is mine. Comments, thoughts and suggestions are certainly appreciated!

Welcome to the new rayners.org!
