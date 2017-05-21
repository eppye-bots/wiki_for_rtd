## edifact character-sets (UNOA, UNOB, etc)

Edifact uses its own naming of character-sets.  
And some character-sets quite typical or old.

Bots has 2 ways of supporting these edifact character-sets:

1.  via specific character-sets UNOA and UNOB in *bots/usersys/charsets*
2.  in bots.ini aliases are giving for edifact character-sets, eg:
    UNOC=latin1=iso8859-1


There are some problems with character-sets UNOA and UNOB:

-   this is not always handle correct by some, eg they send UNOA with
    lower-case characters.
-   in practice often is send; officially these are not in UNOA or
    UNOB.
-   etc

A default bots installation includes by default the UNOA and UNOB
character set. These are not strict interpreted, but 'tuned to reality',
so that they will not often lead to problems.

In the download 'charsetvariations' on [sourceforge
site](http://sourceforge.net/projects/bots/files/grammars/edifact%20grammars/)
are some variations on these character-sets (stricter, less strict).
Read the comments in these files first.


