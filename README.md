stash-bash
==========

Stash Bash is a system for saving shell functions in bash. Don't lose those
bash functions you put effort into creating, just by closing a window.

Let's say you create a function to work out the so-called "extension" of
a filename, that is, the text after the full stop, if any:

    bash$ extension () { echo "$*" | awk -F. 'NF > 1 {print $NF}'; }

You may not be aware that you can get bash to echo this definition back
to your terminal, thus:

    bash$ declare -f extension
    extension () 
    { 
        echo "$*" | awk -F. 'NF > 1 {print $NF}'
    }

Stash Bash saves these for you in a directory under $HOME:

    bash$ stash extension
    bash$ cat ~/.stash-bash/extension
    extension () 
    { 
        echo "$*" | awk -F. 'NF > 1 {print $NF}'
    }

Since you might want to create functions which rely on other functions you've
defined, there's a facility for expressing dependencies, which is consulted
by the tool which loads all your functions into a new shell. That file
is called ~/.stash-bash/_depends , and is run through [tsort](http://en.wikipedia.org/wiki/Tsort_(Unix%29)

Load it all back in with

    bash$ . ~/bin/load-all

