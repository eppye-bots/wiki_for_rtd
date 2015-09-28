Migrate from Kid to Genshi for templates
========================================

If you use bots edi type *template* then you are using kid for those
templates. From version 2.1.0 onwards, using Genshi is also supported,
using edi type *template-html*. In a future bots version, kid will be
removed as it is no longer being developed.

You may have copied templates from a plugin, or developed your own. Each
template normally consists of three files: \*
*usersys/grammars/template/\ ``<messagetype``>.py* is the grammar
configured in the translation and defines the actual template files
used. \* *usersys/grammars/template/templates/\ ``<messagetype``>.kid*
is the template containing html code for the main body of the message.
\*
*usersys/grammars/template/templates/\ ``<messagetype``>\ ``_``\ envelope.kid*
is the envelope template containing header and footer html code. \* Your
naming standard for the .kid files may differ from the above example

To convert this to a Genshi template, at least the following steps are
required. There may be additional changes depending on your template
complexity. For more info see `Comparing Genshi to
Kid <http://genshi.edgewall.org/wiki/GenshiVsKid>`__.

1. Of course, the `Genshi <http://genshi.edgewall.org/>`__ library must
   be installed for this to work.
2. Copy the three source files from *usersys/template* to
   *usersys/templatehtml*. The compiled .pyc files are not copied. Keep
   the same */templates* sub-directory structure for the templates.
3. Also copy the *``__``\ init.py\ ``__``* files when first creating
   this new directory structure.
4. Rename the two copied .kid files to .html (ie. just change the file
   extension)
5. Edit the *``<messagetype``>.py* file and change it's *template* and
   *envelope-template* settings that refer to the .kid files to .html
   files.

   ::

       syntax = {
               'charset':'utf-8',
               'contenttype':'text/html',
               'merge':False,
               'template':'<messagetype>.html',
               'envelope-template':'<messagetype>_envelope.html'}

6. Edit the two .html template files and make the following changes:

   -  Namespaces should be changed

      ::

          <!-- Kid namespace --> 
          <html xmlns:py="http://purl.org/kid/ns#">

      ::

          <!-- Genshi namespaces (xmlns:xi probably needed only in envelope) -->
          <html xmlns:py="http://genshi.edgewall.org/" xmlns:xi="http://www.w3.org/2001/XInclude">

   -  xi:include should be used instead of py:replace in the envelope
      template \`\`\`

      .. raw:: html

         <div py:strip="True" py:for="message in data">
         <div py:replace="document(message)"/>

.. raw:: html

   </div>

::

.. raw:: html

   <!-- Genshi syntax for include -->
   <div py:strip="True" py:for="message in data">
       

.. raw:: html

   </div>

\`\`\` 1. Change your translation: change template to template-html. 1.
Last, but not least: test this ;-)
