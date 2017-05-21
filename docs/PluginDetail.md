## Details about plugins 

-   A plugin is just a zip-file, you can view the contents.
-   A plugin has to contain a file (at the root) called _botsindex_. This contains the database configuration.
-   The plugins on the web-site contain example edi files so you can run a translation and see the results.
-   The edi files are in _bots/botssys/infile_; the results will be in _bots/botssys/outfile_.
-   When reading a plugin your existing current configuration is backupped (in _bots/botssys_)
-   When reading a plugin already existing database-entries, mapping scripts, grammars etc are overwritten.
-   In the web server log is logged what is installed (logging is in _bots/botssys/logging_).
-   There is no un-install.
-   Beware if you make a plugin and share this: do not use e.g. password for an email account.
-   Plugins contain source code. This is a potentially security risk. Use only plugins from trusted sources.
-   Grammars for edifact and x12 are NOT plugins, and can not be installed!