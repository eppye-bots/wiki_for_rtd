## Translate to multiple versions of edi message 

Information about the version is in in-house-message. 

- 	one grammar for in-house message: 
	-	myinhouseorder.py 
	
-	grammars for both versions: 
	- 	ORDERSD93AUN 
	-	ORDERSD96AUN 
    
-	in grammar myinhouseorder.py: use
	QUERIES to extract 'alt'. 
    
- 	use 2 translation rules 
	- 	fixed-myinhouseorder /ORDERSD963AUNEAN007 to edifact/ ORDERSD93AUNEAN007 with
		mapping script ordersfixed2edifact93.py 
    -	translate fixed/ORDERSD96AUNEAN008 to edifact/ ORDERSD96AUNEAN008 with mapping
		script ordersfixed2edifact96.py for alt 'other translation'

### Translate message and send a confirmation

see [Confirmations/acknowledgements](Confirmations.md)

