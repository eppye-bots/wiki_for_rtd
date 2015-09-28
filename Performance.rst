Notes: \* Most edi files are just a few kilobyes. An edi file of 5Mb is
very large (edifact, x12). If you encounter larger ones: please let me
know. \* AFAIK there are no issues with performance. If you run into
this: please inform me eg via mailing list.

.. raw:: html

   <h3>

More performance

.. raw:: html

   </h3>
   <ol><li>

(Bots >= 2.2.0) Cdecimals (Extern library) speeds up bots. This library
will be included in python 3.3, but can be installed in earlier python
versions. See website

.. raw:: html

   </li><li>

(bots >= 3.1) Do not use get\_checklevel=2 in config/bots.ini. This does
extended checking of mpath's, use this during development only.

.. raw:: html

   </li><li>

(bots >= 3.0) Schedule bots-engine via the job queue server.

.. raw:: html

   </li><li>

For xml: check if the c-version of python's elementtree is installed and
used.

.. raw:: html

   </li><li>

Enough memory is important for performance: disk-memory swapping is
slow! Actual memory usage depends on size of edi-files.

.. raw:: html

   </li><li>

Check mappings for slow/inefficient algorithms.

.. raw:: html

   </li><li>

Bots works with [www.pypy.org pypy], see below on this page.

.. raw:: html

   </li><li>

Use SSD for faster reading/writing. In config/bots.ini the
botssys-directory can be set, in config/settings.py the place of the
SQLite-database.

.. raw:: html

   </li></ol>

.. raw:: html

   <h3>

Strategy for bigger edi volumes

.. raw:: html

   </h3>
   <ol><li>

Best strategy is to schedule bots-engine more often.

.. raw:: html

   </li><li>

(bots >= 3.0) Schedule bots-engine via the job queue server.

.. raw:: html

   </li><li>

Routes can be scheduled independently.

.. raw:: html

   </li><li>

Set-up good scheduling, keeping volumes in mind.

.. raw:: html

   <ul><li>

edi in the real world has often large peaks.

.. raw:: html

   </li><li>

some edi transactions are time critical (eg orders), others not so much
(eg invoices)

.. raw:: html

   </li><li>

check where the large volumes are (size and number of edi-transactions)

.. raw:: html

   </li><li>

look at the sending pattern of your customers. Often edi is send in
night jobs, so you might receive lot of volume early in the morning.

.. raw:: html

   </li><li>

check where you send large volumes. Send this at a time that does not
interfere with other flows.

.. raw:: html

   </li></ul></li><li>

Incoming volumes can be limited per run. This way the time bots-engine
runs is predictable. The max time a channel fetches incoming files is a
parameter for each channel. Note: this is dependent upon the
communication type used; eg file system I/O is much faster than SFTP.
Files "left behind" will be fetched on subsequent runs.

.. raw:: html

   </li><li>

(Bots >= 3.0) Limit for max file-size (set in bots.ini). If an incoming
file is larger, bots will give error. This is to prevent 'accidents'.

.. raw:: html

   </li></ol>

.. raw:: html

   <h3>

Performance/throughput testing

.. raw:: html

   </h3>
   <ol><li>

Tests are done using file system I/O (no testing of communication
performance).

.. raw:: html

   </li><li>

Tests done in one run of bots-engine.

.. raw:: html

   </li><li>

Test system: Intel Q9400 2.66GHz; 4Gb memory; ubuntu 10.04(lucid);
python 2.7; default SQLite database.

.. raw:: html

   </li><li>

Please note that these tests are 'artificial': if you have such high
volumes and big files look at good scheduling!

.. raw:: html

   </li><li>

test are with edifact; x12 performance is the same.

.. raw:: html

   </li></ol>

   <table><thead><th> </th><th>  </th><th> </th><th> </th><th> 

bots2.0

.. raw:: html

   </th><th> </th><th> 

bots2.2

.. raw:: html

   </th><th> 

(cdecimal)

.. raw:: html

   </th><th> 

bots3.2

.. raw:: html

   </th><th> </th></thead><tbody>
   <tr><td> 

description

.. raw:: html

   </td><td> 

#file

.. raw:: html

   </td><td> 

vol

.. raw:: html

   </td><td> 

#mess.

.. raw:: html

   </td><td> 

time

.. raw:: html

   </td><td> </td><td> 

time

.. raw:: html

   </td><td>                  </td><td> 

time

.. raw:: html

   </td><td> </td></tr>
   <tr><td>

01 edifact2fixed

.. raw:: html

   </td><td>

32

.. raw:: html

   </td><td>

305Mb

.. raw:: html

   </td><td>

32

.. raw:: html

   </td><td>

1:01:39

.. raw:: html

   </td><td>

82 kb/s

.. raw:: html

   </td><td>

0:50:57

.. raw:: html

   </td><td> 

100 kb/s

.. raw:: html

   </td><td>

0:44:01

.. raw:: html

   </td><td> 

115 kb/s

.. raw:: html

   </td></tr>
   <tr><td>

02 edifact2fixed

.. raw:: html

   </td><td>

116

.. raw:: html

   </td><td>

300Mb

.. raw:: html

   </td><td>

116

.. raw:: html

   </td><td>

1:14:18

.. raw:: html

   </td><td>

68 kb/s

.. raw:: html

   </td><td>

0:36:20

.. raw:: html

   </td><td>

137 kb/s

.. raw:: html

   </td><td>

0:37:25

.. raw:: html

   </td><td> 

133 kb/s

.. raw:: html

   </td></tr>
   <tr><td>

03 edifact2fixed

.. raw:: html

   </td><td>

94048

.. raw:: html

   </td><td>

295Mb

.. raw:: html

   </td><td>

141072

.. raw:: html

   </td><td>

0:47:21

.. raw:: html

   </td><td>

104 kb/s

.. raw:: html

   </td><td>

0:39:54

.. raw:: html

   </td><td>

125 kb/s

.. raw:: html

   </td><td>

0:42:30

.. raw:: html

   </td><td> 

115 kb/s

.. raw:: html

   </td></tr>
   <tr><td>

04 fixed2edifact

.. raw:: html

   </td><td>

14244

.. raw:: html

   </td><td>

300Mb

.. raw:: html

   </td><td>

78342

.. raw:: html

   </td><td>

1:04:11

.. raw:: html

   </td><td>

78 kb/s

.. raw:: html

   </td><td>

0:33:21

.. raw:: html

   </td><td>

150 kb/s

.. raw:: html

   </td><td>

0:32:40

.. raw:: html

   </td><td> 

153 kb/s

.. raw:: html

   </td></tr>
   <tr><td>

05 xml2edifact

.. raw:: html

   </td><td>

17424

.. raw:: html

   </td><td>

300Mb

.. raw:: html

   </td><td>

17424

.. raw:: html

   </td><td>

0:41:24

.. raw:: html

   </td><td>

121 kb/s

.. raw:: html

   </td><td>

0:35:48

.. raw:: html

   </td><td>

139 kb/s

.. raw:: html

   </td><td>

0:35:20

.. raw:: html

   </td><td> 

141 kb/s

.. raw:: html

   </td></tr>
   <tr><td>

06 edifact2xml(1to1)

.. raw:: html

   </td><td>

14609

.. raw:: html

   </td><td>

300Mb

.. raw:: html

   </td><td>

74919

.. raw:: html

   </td><td>

1:23:03

.. raw:: html

   </td><td>

60 kb/s

.. raw:: html

   </td><td>

0:58:19

.. raw:: html

   </td><td>

85 kb/s

.. raw:: html

   </td><td>

0:44:38

.. raw:: html

   </td><td> 

112 kb/s

.. raw:: html

   </td></tr></tbody></table>

 Conclusions of performance measurements

.. raw:: html

   <ol><li>

Memory usage is stable (no leakage).

.. raw:: html

   </li><li>

Memory usage is directly related to the size of the edi-files. In test
01 (edifact files of 9.5Mb) bots-engine uses 1.5Gb memory.

.. raw:: html

   </li><li>

Tested with edifact files of 120Mb; memory usage is stable at 4.5Gb.

.. raw:: html

   </li><li>

Performance is reasonably independent from the size of
edi-files/messages.

.. raw:: html

   </li><li>

an edifact file of 9.5Mb takes about 85sec to be processed.

.. raw:: html

   </li><li>

for outgoing edi files: writing to one file or multiple file does not
significantly affect performance.

.. raw:: html

   </li></ol>

.. raw:: html

   <h3>

Testing with pypy

.. raw:: html

   </h3>

[www.pypy.org Pypy] is a python implementation that is faster by using a
JIT (that is one of their achievements...). Results of the first tests
with pypy (beta-versions of pypy 2.0):

.. raw:: html

   <ul><li>

Bots works with pypy.

.. raw:: html

   </li><li>

Comparing some stress tests: much faster, 2-3 times faster.

.. raw:: html

   </li><li>

Did not run all test-sets. Probably I will do that with definitive
version of pypy 2.0 and/or release of bots 3.1.

.. raw:: html

   </li><li>

Problem might be that not all libraries/dependencies work with pypy.

.. raw:: html

   <ul><li>

SQLite3 database connector: OK

.. raw:: html

   </li><li>

MySQL database connector: version 1.2.5 does. Note that bots 3.1.0 gave
am error with this version, a patch was easy.

.. raw:: html

   </li><li>

paramiko (for SFTP/SSH): no, dependency pycrypto is not supported. This
looks like a very interesting development!
