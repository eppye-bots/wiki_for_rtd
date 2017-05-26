Deployment
==========

This part of the wiki is about using bots in production.
There are extra points to consider when deploying bots in a 24x7 production environment:

#. Consider the best way of :doc:`running bots-engine <run-botsengine>`.
#. When errors in edi-files occur, receive a :doc:`notification by email <email-notifications>`.
#. :doc:`Use multiple environments <multiple-environments>`; having different environments for at least test and production is standard IT practice.
#. Consider if you need :doc:`extra archiving <archiving>` fro edi files.
#. Install bots as a :doc:`service/daemon <run-as-service>`.
#. Use limited rights for users.
#. If you use bots-monitor over the internet/outside your LAN, use HTTPS/SSL connection.
#. use apache as web server (instead of default cherrypy)
#. Use MySQL or PostgreSQL as database for Bots. 
#. Use AS2 as communication method.
#. Bots has options to push changes from test to production.


.. toctree::
    :maxdepth: 2
    :hidden:

    run-botsengine
    production-errors
    email-notifications
    archiving
    run-as-service
    multiple-environments
    user-rights
    bots-https
    use-apache2
    use-mysql
    use-as2
    change-management
