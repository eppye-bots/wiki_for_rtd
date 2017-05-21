## Migrate from Kid to Genshi for templates

If you use bots edi type \_template\_ then you are using kid for those 
templates. From version 2.1.0 onwards, using Genshi is also supported, 
using edi type \_template-html\_. In a future bots version, kid will be 
removed as it is no longer being developed. 

You may have copied templates from a plugin, or developed your own. 
Each template normally consists of three files: 

-	_usersys/grammars/template/`<messagetype>`.py_ is the grammar configured
	in the translation and defines the actual template files used. 
-	_usersys/grammars/template/templates/`<messagetype>`.kid_ is the template
	containing html code for the main body of the message. 
-	_usersys/grammars/template/templates/`<messagetype>`\_envelope.kid_ is the
	envelope template containing header and footer html code. 
-	Your naming standard for the .kid files may differ from the above example 

To convert this to a Genshi template, at least the following steps are required.
There may be additional changes depending on your template complexity.
For more info see [Comparing Genshi to
Kid](http://genshi.edgewall.org/wiki/GenshiVsKid). 

1.	Of course, the [Genshi](http://genshi.edgewall.org/) library must be 
	installed for this to work. 
1. 	Copy the three source files from _usersys/template_ to
	_usersys/templatehtml_. The compiled .pyc files are not copied. Keep
	the same _/templates_ sub-directory structure for the templates. 
1.	Also copy the _\_\_init.py\_\__ files when first creating this
	new directory structure. 
1.	Rename the two copied .kid files to .html (ie. just change the file extension) 
1. 	Edit the _`<messagetype>`.py_ file and change it's _template_ and _envelope-template_ settings that refer
	to the .kid files to .html files. 
    
```python
syntax = { 
	'charset':'utf-8',
	'contenttype':'text/html', 
    'merge':False, 
    'template':'<messagetype>.html',
	'envelope-template':'<messagetype>_envelope.html'} 
``` 

1.	Edit the two .html template files and make the following changes: 
	-	Namespaces should be changed 
    
```html
<!-- Kid namespace -->
<html xmlns:py="http://purl.org/kid/ns#">
```


``` 
* xi:include should be used instead of py:replace in the envelope template 
```

```html
<!-- Kid syntax for replace -->
<div py:strip="True" py:for="message in data">
    <div py:replace="document(message)"/>
</div>
```

```html
<!-- Genshi syntax for include -->
<div py:strip="True" py:for="message in data">
    <xi:include href="${message}" />
</div>
``` 

1.	Change your translation: change template to template-html. 
1.	Last, but not least: test this ;-)
	