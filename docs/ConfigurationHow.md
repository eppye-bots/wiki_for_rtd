## How do I make an edi configuration?

1.  Use [plugins](PluginIntroduction.md). This is a quick and easy way to install predefined configurations of bots.
    -   Downloads: [bots sourceforge site](http://sourceforge.net/projects/bots/files/plugins/)
    -   Description of plugins: [on this wiki page](PluginList.md)
    -   Plugins can be shared by users and communities. Send your plugin!
1.  Use a plugin 'close' to what you want, and adapt.
1.  Do your own configuration:
    -   Take a look at [the tutorial](StartMyFirstPlugin.md).
    -   Use bots-monitor for configuration of routes, channels, translations and partners.
    -   There are grammars for all edifact and x12 messages 
        [on the bots sourceforge site](http://sourceforge.net/projects/bots/files/grammars/).
    -   Grammars and mapping require knowledge of edi and edi-standards and some python knowledge. 
        (python is a relatively easy programming, no deep knowledge of python is needed).
    -   Use command line tool 'bots-xml2botsgrammar.py' to generate a grammar from an xml file.
    -   Check a grammar using the command line tool 'bots-grammar.py'.
1.  A step by step [description](ConfigurationDIY.md) of making a configuration.
1.  If you are doing your own configuration check out [how to debug](Debug.md)
1.  Hire us ([EbbersConsult](http://www.ebbersconsult.com) - the makers of Bots) to help you with configuring bots: we are the edi experts.