---
layout: post
title:  "vim summer notes mmxx"
date:   2020-07-26 21:34:34 +0200
categories: vim remagent
---

![gras](/assets/img/vim-manual.png)

Vacation time. I'm re-reading the vim documentation and taking note of stuff I haven't already started to use that looks useful. I was thinking of looking up how to do good project searching in vim, and noting it down in a gist - but maybe revive this site for quick lookup.

Setting up this blog is also related to the idea of the remembrance agent. I will try to make my own notes of the stuff I need to look up on google, I usually dump the gist of such searches to a directory of text files, but - a blog could come in handy and be used across computers.

Also I don't want to rely on a super customized .vim folder, so I can be able to easily use vim on a server. However there are some plugins that I find useful that I will have installed:

 * nerdtree
 * syntastic

anyhow, these are my notes so that I can look this up and remember

## stdout & stdin 

read output from shell command to vim

{% highlight vim %}
:read !ls
{% endhighlight %}

reverse write to a shell command

{% highlight vim %}
:write !wc
{% endhighlight %}

## man pages

I've sometimes managed to accidentally trigger the man page view when using vim, but I have not looked into actually using the feature. I do frequently use the man pages for C reference when writing programs though, but I do trigger them from the shell. To view a man page for a function in C press 'K' with cursor on function. Reading on in the manual it suggests enabling the ftplugin for man, tried it out and it looks promising so I added it. The benefit of using the filetype plugin is that it would open in a split view. I have the leader mapped to ',' so opening the man page in split view would then be ',K' 

Interesting that the man pages command is on such a central key in vim, but then the man pages are so central to unix. I love how well-behaved C libraries like [libdill] provide man pages for their api.

{% highlight vim %}
" use :Man strcmp or similar to open man page in split view, 
" K to view for function under cursor, leader ,K (to open in split)
runtime! ftplugin/man.vim
{% endhighlight %}

## grepping with vim

I tend to CTRL-Z out of vim and use grep and ack to search files, when I could be using the built in search, and the clist to show hits. I've felt that being able to quickly redo the search with the -A -B -C switches outweights the benefits of the the built in hits list. 

Search in vim is very slow if not using the variant that uses external grep on external tools though.

{% highlight sh %}

The internal method will be slower, because files are read into memory.

5.2 External grep

Vim can interface with "grep" and grep-like programs (such as the GNU
id-utils) in a similar way to its compiler integration (see |:make| above).

[Unix trivia: The name for the Unix "grep" command comes from ":g/re/p", where
"re" stands for Regular Expression.]

{% endhighlight %}


{% highlight bash %}
:grep -r --include \*.h --include \*.c ipaddr_local .
# -- or -- 
:grep -r --include=\*.{c,h} ipaddr_local .
{% endhighlight %}

this goes for a quite complicated command.. maybe change to ack, and how to get the quickfix list up smoothly?

{% highlight sh %}
:cnext
:clist
:cwindow # display quickfix list
{% endhighlight %}

## make

vim's built in :make support, :cwindow :)

makes it super easy to build from vim and jump to the offending line if build error

## CTRL-O  -- (insert) --

execute any normal mode command in insert mode 

## CTRL-L 

redraw screen

## search pattern start and end of word 

 * use ```\<``` to match start of word
 * use ```\>``` to match end of word

[libdill]: http://libdill.org
