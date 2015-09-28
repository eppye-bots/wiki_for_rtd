Partner dependent syntax
------------------------

For outgoing messages it is possible to specify a partner dependent
syntax. This is especially useful for x12 and edifact, for setting
envelope values and partner specific separators. These parameters
override the settings in the message grammar; you only need to specify
the partner-specific parameters. Note: no need to set partner specific
separators for incoming messages; bots will figure this out by itself.

To set partner specific syntax parameters, create according to editype
used:

.. raw:: html

   <ul><li>

bots/usersys/partners/x12/partnerid.py

.. raw:: html

   </li><li>

bots/usersys/partners/edifact/partnerid.py

.. raw:: html

   </li></ul>

Example file with partner specific setting (x12):

.. raw:: html

   <blockquote><pre><code><br>
   syntax = {<br>
   'ISA05'                  : 'XX',    #use different communication qualifier for sender<br>
   'ISA07'                  : 'ZZ',    #use different communication qualifier for receiver<br>
   'field_sep'              : '|',     #use different field separator<br>
   }<br>
   </code></pre></blockquote>

Example file with partner specific setting (edifact):

.. raw:: html

   <blockquote><pre><code><br>
   syntax = {<br>
   'merge':False,<br>
   'forceUNA':True,<br>
   'UNB.S002.0007':'ZZ',        # partner qualifier<br>
   'UNB.S003.0007':'ZZ',        # partner qualifier<br>
   }<br>
   </code></pre></blockquote>

.. raw:: html

   <h3>

Plugin

.. raw:: html

   </h3>

Plugin 'demo\_partnerdependent' at the bots sourceforge site
demonstrates partner dependent syntax.

.. raw:: html

   <h2>

Relevant x12 syntax settings

.. raw:: html

   </h2>
   <table><thead><th> 

Name

.. raw:: html

   </th><th> 

Default

.. raw:: html

   </th><th> 

Description

.. raw:: html

   </th></thead><tbody>
   <tr><td>

ISA05

.. raw:: html

   </td><td>

01

.. raw:: html

   </td><td>

Interchange ID Sender Qualifier

.. raw:: html

   </td></tr>
   <tr><td>

ISA07

.. raw:: html

   </td><td>

01

.. raw:: html

   </td><td>

Interchange ID Receiver Qualifier

.. raw:: html

   </td></tr>
   <tr><td>

ISA15

.. raw:: html

   </td><td>

P

.. raw:: html

   </td><td>

Testindicator: P(roduction) or T(est); mostly set per
message/transaction.

.. raw:: html

   </td></tr>
   <tr><td>

GS07

.. raw:: html

   </td><td>

X

.. raw:: html

   </td><td>

Responsible Agency Code

.. raw:: html

   </td></tr>
   <tr><td>

version

.. raw:: html

   </td><td>

00403

.. raw:: html

   </td><td>

As ISA12

.. raw:: html

   </td></tr>
   <tr><td>

functionalgroup

.. raw:: html

   </td><td>                </td><td>

As GS01; set this for each x12 messagetype

.. raw:: html

   </td></tr>
   <tr><td>

record\_sep

.. raw:: html

   </td><td>

~

.. raw:: html

   </td><td>

Segment terminator.

.. raw:: html

   </td></tr>
   <tr><td>

field\_sep

.. raw:: html

   </td><td> 

\*

.. raw:: html

   </td><td>                    </td></tr>
   <tr><td>

sfield\_sep

.. raw:: html

   </td><td>

    ::

                  </td><td>Sub-field separator (in composites).</td></tr>

    .. raw:: html

       <tr><td>

    merge

    .. raw:: html

       </td><td>

    True

    .. raw:: html

       </td><td>

    Merge messages to envelopes (False: no merging, only envelope).

    .. raw:: html

       </td></tr>
       <tr><td>

    add\_crlfafterrecord\_sep

    .. raw:: html

       </td><td>

    .. raw:: html

       </td><td>

    Adds CR/LF after each segment.

    .. raw:: html

       </td></tr></tbody></table>

.. raw:: html

   <h2>

Relevant edifact syntax settings

.. raw:: html

   </h2>
   <table><thead><th> 

Name

.. raw:: html

   </th><th> 

Default

.. raw:: html

   </th><th> 

Description

.. raw:: html

   </th></thead><tbody>
   <tr><td>

UNB.S002.0007

.. raw:: html

   </td><td>

14

.. raw:: html

   </td><td>

Identification code qualifier

.. raw:: html

   </td></tr>
   <tr><td>

UNB.S002.0008

.. raw:: html

   </td><td>                </td><td>

Interchange sender internal identification

.. raw:: html

   </td></tr>
   <tr><td>

UNB.S002.0042

.. raw:: html

   </td><td>                </td><td>

Interchange sender internal sub-identification

.. raw:: html

   </td></tr>
   <tr><td>

UNB.S003.0007

.. raw:: html

   </td><td>

14

.. raw:: html

   </td><td>

Identification code qualifier

.. raw:: html

   </td></tr>
   <tr><td>

UNB.S003.0014

.. raw:: html

   </td><td>                </td><td>

Interchange recipient internal identification

.. raw:: html

   </td></tr>
   <tr><td>

UNB.S003.0046

.. raw:: html

   </td><td>                </td><td>

Interchange recipient internal sub-identification

.. raw:: html

   </td></tr>
   <tr><td>

UNB.S005.0022

.. raw:: html

   </td><td>                </td><td>

Recipient reference/password

.. raw:: html

   </td></tr>
   <tr><td>

UNB.S005.0025

.. raw:: html

   </td><td>                </td><td>

Recipient reference/password qualifier

.. raw:: html

   </td></tr>
   <tr><td>

UNB.0026

.. raw:: html

   </td><td>                </td><td>

Application reference

.. raw:: html

   </td></tr>
   <tr><td>

UNB.0029

.. raw:: html

   </td><td>                </td><td>

Processing priority code

.. raw:: html

   </td></tr>
   <tr><td>

UNB.0031

.. raw:: html

   </td><td>                </td><td>

Acknowledgement request

.. raw:: html

   </td></tr>
   <tr><td>

UNB.0032

.. raw:: html

   </td><td>                </td><td>

Interchange agreement identifier (eg. EANCOM)

.. raw:: html

   </td></tr>
   <tr><td>

UNB.0035

.. raw:: html

   </td><td>

0

.. raw:: html

   </td><td>

Testindicator. Mostly set per message.

.. raw:: html

   </td></tr>
   <tr><td>

charset

.. raw:: html

   </td><td>

UNOA

.. raw:: html

   </td><td>

As S001.0001

.. raw:: html

   </td></tr>
   <tr><td>

version

.. raw:: html

   </td><td>

3

.. raw:: html

   </td><td>

As S001.0002

.. raw:: html

   </td></tr>
   <tr><td>

merge

.. raw:: html

   </td><td>

True

.. raw:: html

   </td><td>

Merge messages to envelopes (False: no merging, only envelope).

.. raw:: html

   </td></tr>
   <tr><td>

forceUNA

.. raw:: html

   </td><td>

False

.. raw:: html

   </td><td>

Always use UNA in outgoing edifact, even if not strictly needed.

.. raw:: html

   </td></tr>
   <tr><td>

add\_crlfafterrecord\_sep

.. raw:: html

   </td><td>

.. raw:: html

   </td><td>

Adds CR/LF after each segment.

.. raw:: html

   </td></tr>

