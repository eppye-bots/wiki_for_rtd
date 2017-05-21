## Introduction

> Definition: _A translation translates a
message of a certain editype, messagetype to another editype,
messagetype_ 

Needed for a translation: 

1. 	Translation rule in _bots-monitor-\>Configuration-\>Translations_; see the screen shot
	below. 
1. 	[Grammar](GrammarsIntroduction.md) for incoming message. 
1.	[Grammar](GrammarsIntroduction.md) for outgoing message. 
1. 	Mapping script that for converting incoming message to outgoing message.

> *Screenshot of configured translations-rules*

> ![](TranslationScreenshot1.png)

Read the 1st translation rule of this screen shot:

> translate edifact-ORDERSD96AUNEAN008 to fixed-myinhouseorder using
> mapping script ordersedifact2myinhouse.py
