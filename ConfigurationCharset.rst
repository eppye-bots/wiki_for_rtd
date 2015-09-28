edifact character-sets (UNOA, UNOB, etc)
----------------------------------------

Edifact uses its own naming of character-sets. And some character-sets
quite typical or old. Bots has 2 ways of supporting these edifact
character-sets:

.. raw:: html

   <ol><li>

via specific character-sets UNOA and UNOB in bots/usersys/charsets

.. raw:: html

   </li><li>

in bots.ini aliases are giving for edifact character-sets, eg:
UNOC=latin1=iso8859-1

.. raw:: html

   </li></ol>

 There are some problems with character-sets UNOA and UNOB:

.. raw:: html

   <ul><li>

this is not always handle correct by some, eg they send UNOA with
lower-case characters.

.. raw:: html

   </li><li>

in practice often is send; officially these are not in UNOA or UNOB.

.. raw:: html

   </li><li>

etc

.. raw:: html

   </li></ul>

A default bots installation includes by default the UNOA and UNOB
character set. These are not strict interpreted, but 'tuned to reality',
so that they will not often lead to problems. In the download
'charsetvariations' on sourceforge site are some variations on these
character-sets (stricter, less strict). Read the comments in these files
first.
