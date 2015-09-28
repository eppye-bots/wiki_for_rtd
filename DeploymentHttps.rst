Bots-monitor over HTTPS Introduction
====================================

This feature is introduced in bots 2.1.0. This works with cherrypy >
3.2.0 in combination with python 2.6 or 2.7. In python 2.5 this works
(using extra dependency pyOpenssl) but gives problems with reading
plugins. Procedure:

.. raw:: html

   <ol><li>

you will need an SSL certificate. You can use self-signed certificates.

.. raw:: html

   </li><li>

in bots/config/bots.ini uncomment options ssl\_certificate and
ssl\_private\_key (in section webserver), and set these to the right
value, eg:

.. raw:: html

   <pre><code>ssl_certificate = /mysafeplace/mycert.pem <br>
   ssl_private_key = /mysafeplace/mycert.pem<br>
   #In this example certificate and private key are in the same pem-file.<br>
   </code></pre>
   </li><li>

restart bots-webserver

.. raw:: html

   </li><li>

point your browser to the right https-address, eg:
https://localhost:8080

.. raw:: html

   </li></ol>

   <h3>

Tips

.. raw:: html

   </h3>

If you are using cherrypy and receive an error
"ssl\_error\_rx\_record\_too\_long" try the 2-line fix at
https://bitbucket.org/cherrypy/cherrypy/issue/1293/ssl-broken-under-pypy-221

You can create self-signed certificates at
http://www.selfsignedcertificate.com/

You can configure port=443 in bots.ini then just point your browser to
https://localhost
