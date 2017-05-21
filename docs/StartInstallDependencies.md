## Dependencies

### Always needed
-   Needs: python 2.6/2.7. Python 2.5 works but extra dependencies are needed. Python >= 3.0 does not work.
-   Needs: django >= 1.4.0, django <= 1.7.0
-   Needs: cherrypy > 3.1.0

### Optional
-   Genshi (when using templates/mapping to HTML).
-   SFTP needs paramiko and pycrypto. Newer versions of paramiko also need ecdsa.
-   Cdecimals speeds up bots. See [website](http://www.bytereef.org/mpdecimal/index.html)
-   bots-dirmonitor needs:
    -   pyinotify on `*`nix
    -   Python for Windows extensions (pywin) for windows
-   xlrd (when using incoming editype 'excel').
-   mysql-Python >= 1.2.2, MySQL (when using database MySQL).
-   psycopg2, PostgreSQL (when using database PostgreSQL).
