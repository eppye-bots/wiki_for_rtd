## Configuration Overview

Out of the box bots does nothing. You have to configure bots for your
specific edi requirements.  
Check out different ways to [start your own configuration](ConfigurationHow.md).  
See [debug overview](Debug.md) for info how to debug while making a
configuration.  
Bots also has nice features for [configuration change management](DeploymentEnv.md) 
(build test sets for you configuration, easier pushing of changes from test to 
production).



### Configuration explained in short

-   'routes' are edi-workflows.
-   'channels' do the communication (from file system, ftp, etc).
-   each route hs an 'inchannel' and an 'outchannel'
-   Translations rules determine: translate what to what.



### Most asked configuration topics

-	[composite routes](RoutesComposite.md)
-	[passthrough route](RoutesPass.md) (without translation)
-	[options for outgoing filenames](Filenames.md)
-	[direct database communication](ChannelsDatabase.md)
-	[partner specific translations](TranslationperPartner.md)
-	[code conversion](MappingCcode.md)
-	view [business documents](ConfigurationBotskey.md) instead of edi-files.
-	[confirmations/acknowledgements](Confirmations.md)
-	[merging and enveloping outgoing edi files](ConfigurationMerge.md)
-	[partner specific syntax](GrammarsPartnerSyntax.md) (especially for x12
	and edifact)

