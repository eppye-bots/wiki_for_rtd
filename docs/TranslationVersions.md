## Translation Versions

Several situations: 

-	send different versions of messages 
-	receive different versions Note: in real world versions are often so similar
	that the same mapping script can be used (or a simple if-then can cater
	for the differences).

### Send multiple versions using partners

use the 'topartner' to determine the right version to send.

-   one grammar for in-house message:
    -   myinhouseorder.py
    -   this grammar uses QUERIES to extract 'topartner'.
-   grammars for both versions:
    -   ORDERSD93AUN
    -   ORDERSD96AUN
-   2 translation rules:
    -   fixed-myinhouseorder to edifact-ORDERSD93AUN using mapping
        script ordersfixed2edifact93.py for topartner=XXX
    -   fixed-myinhouseorder to edifact-ORDERSD96AUN using mapping
        script ordersfixed2edifact93.py for topartern=YYY


### Send multiple versions using alt

Information about the version is in in-house-message: a field that
contains either '93' or '96'.

-   one grammar for in-house message:
    -   myinhouseorder.py
-   grammars for both versions:
    -   ORDERSD93AUN
    -   ORDERSD96AUN
-   2 translation rules
    -   fixed-myinhouseorder to edifact-ORDERSD93AUN using mapping
        script orders\_fixed2edifact93.py for alt=93
    -   fixed-myinhouseorder to edifact-ORDERSD96AUN using mapping
        script orders\_fixed2edifact93.py for alt=96


### Receive multiple versions

grammars for both versions:

-   ORDERSD93AUN
-   ORDERSD96AUN

one grammar for in-house message:

-   myinhouseorder.py
-   this grammar uses QUERIES to extract 'alt'-value.

2 translation rules

-	edifact-ORDERSD93AUN to fixed-myinhouseorder using mapping script
	orders\_edifact93\_2\_fixed.py

-	edifact-ORDERSD6AUN to fixed-myinhouseorder using mapping script
	orders\_edifact96\_2\_fixed.py

