## Bots-monitor over HTTPS Introduction

This feature is introduced in bots 2.1.0.  
This works with cherrypy \> 3.2.0 in combination with python 2.6 or
2.7. In python 2.5 this works (using extra dependency pyOpenssl) but
gives problems with reading plugins.

Procedure:

1.  you will need an SSL certificate. You can use self-signed
    certificates.
2.  in *bots/config/bots.ini* uncomment options ssl\_certificate and
    ssl\_private\_key (in section webserver), and set these to the right
    value, eg:

        ssl_certificate = /mysafeplace/mycert.pem 
        ssl_private_key = /mysafeplace/mycert.pem
        #In this example certificate and private key are in the same pem-file.

3.  restart bots-webserver
4.  point your browser to the right https-address, eg:
    *https://localhost:8080*

### Tips

If you are using cherrypy and receive an error
"ssl\_error\_rx\_record\_too\_long" try the 2-line fix at
<https://bitbucket.org/cherrypy/cherrypy/issue/1293/ssl-broken-under-pypy-221>

You can create self-signed certificates at
<http://www.selfsignedcertificate.com/> 

You can configure port=443 in
bots.ini then just point your browser to *https://localhost*

