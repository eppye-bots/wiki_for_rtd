Debugging
=========

.. rubric::
    Via bots-monitor (GUI)

- The reports-screen gives an overview of what happened in a run.
- If there are process errors in a run, first view the process errors.
- The incoming-screen gives information about the results of each incoming file.
- For each incoming edi-file: view the detail-screen for information about the processing steps for incoming/outgoing edi file. Usage: in incoming-screen move mouse over star at the start of the line; drop-down box appears; choose 'details'.
- View the outgoing files, including communication errors for outgoing files.

.. rubric::
    Extended Debug options

- Set parameter 'get_checklevel' in config/bots.ini. Value '2' = debug: all gets/puts are checked with the grammar(s).\
  For production: use 1 (sanity checks on get/puts) or 0  (fastest, might give strange error-messages. But than: this should have been debugged by you).
- Set parameter 'debug' in config/bots.ini; gives information about the place in the code where the error occurred.
- Logging. Logging can be found in botssys/logging. Parameters in <a href='StartConfigurationFiles.md'>bots.ini</a> can be set to get more debug information:
    - **log_file_level**: set to DEBUG to get extended information.
    - **readrecorddebug**: information about the records that are read and their content.
    - **mappingdebug**: information about the results of get()/put() in the mapping script. 
        .. note::
            In bots 3.0.0 this does not work (bug). Fix: in botsinit.py, line 188 should be: ``botsglobal.logmap = logging.getLogger('engine.map')``
- For some communication protocols set in config/bots.ini eg ftpdebug, smtpdebug, pop3debug. This debug-information is on the console/command line.
- Within mapping script (or other user script) use 'print', output can be viewed on the console/command line.
- Within a mapping script use root.display() to see message content in mapping script. This is not the nicest output, but is definitely what you received or generated.
    - incoming: at the start of the main function ``inn.root.display()``
    - outgoing: at the end of the main function: ``out.root.display()``

    


.. rubric::
    Tips for debugging

- If a run has process errors, first check the process errors!
- Be careful with character-set/encoding:
    - Can your editor handle this? Be careful with editing files and saving these again, you might run into issues with character-set/encodings!
    - Are you familiar with the character-set you use? Are you familiar with eg utf-8? If not, please check this first.
- In reality, edifact and x12 messages contains errors. Especially when **found on internet**; lot of ISA headers for X12 are not OK.
.. note::
    The errors bots gives for incoming edi-files are quite accurate ;-))
