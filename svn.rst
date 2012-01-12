Nutshell
========

BASE Revision
-------------
``BASE`` revision is different from ``HEAD`` revision. ``HEAD`` is the latest
revision in the repository. ``BASE`` is the last revision you have obtained from
the repository. 

When you revert, your workspace go back to matching the ``BASE`` revision. 


Cookbook
========

check where a branch was created from
-------------------------------------

::

  $ svn log -v --stop-on-copy

``--stop-on-copy`` option will let ``svn log`` command stop on the 

create branch
-------------
::

   $ svn copy </path/to/trunk> </path/to/branch> -m "why I create this branch"

``svn copy`` uses a cheap strategy to copy directories, it will not dupliate any
data but just point to the source directory.

   
merge from branch
-----------------
::
    $ svn co /path/to/trunk
    $ svn log --stop-on-copy 	# find out the begin:end revision number
    $ svn merge -r begin:end /path/to/branch # you could also give a specific 

`svn merge` is actually doing the "diff and apply" work, it will first run a
`svn diff` command on given branch against trunk and then apply the differece to
working copy, so it actaully will not preserve the commit history. 

When working on the branch, you may also need to merge from trunk repeatly to
keep things updated. then you may face some confusing conflict when merge branch
back to trunk since something in the branch are already in trunk.


**svn 1.5** added a "automatic merge tracking" to track merge history.
