## Deployment 

This part of the wiki is about using bots in
production.

There are extra points to consider when deploying bots in a 24x7
production environment:

1.  Consider the best way of [running bots-engine](DeploymentEngineOverview.md).
2.  When errors in edi-files occur, [receive a notification by
	email](DeploymentErrorReports.md).
3.  [Use multiple environments](DeploymentMultipleEnvironments.md); having
	different environments for at least test and production is standard IT
	practice.
4.  Consider if edi files need [extra archiving](Archiving.md)
5.  Out of the box bots does not run as a [service/daemon](DaemonProcesses.md). 
	In a production enviroment this is what you'll probably want.
