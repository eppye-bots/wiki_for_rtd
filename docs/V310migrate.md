## Migrate to version 3.1.0 (from 3.0.0)

### Editype x12: in ISA definition 'ISA11' has to be conditional

Bots 3.1.0 supports the repeating character (for ISA-versions \>=
00403).  
If you use this, ISA11 has to be conditional in definition; file
usersys/grammars/x12/envelope.py:  
was:  
 `['ISA11','M',(1,1),'AN'],`  
becomes in 3.1.0:  
 `['ISA11','C',(1,1),'AN'],`  
This change also works for older ISA-version. Advised is to use this.


### Editype x12, edifact, tradacoms: different handling of syntax parameters

Bots handles the syntax parameters differently. In bots 3.0 and earlier
this was somewhat 'fuzzy'.  
This works now like:  
*default syntax parameters are overruled by envelope parameters,*  
are overruled by message parameters,  
are overruled by frompartner parameters,  
are overruled by topartner parameters.  
Most common problem will be for x12: message grammars had by default in
syntax parameters:  
 `'version'    :  '00403',`  
Formerly this was not used; now it is used.  
This might lead to sending another version of ISA-envelope, this is
probably not what you want!  
Solution: delete (or uncomment) the 'version' syntax parameter for
message grammar.  

Note: the ISA-version you send now is probably in
usersys/grammars/x12/x12.py


### Editype fixed and idoc: 'startrecordID' and 'endrecordID' not longer used

Bots calculates this automatically now. 
Bots also checks for all used records if this is used the same over all
records.  
This might lead to errors.  
Solution: BOTSID should have correct length in all records and be at
correct position.  


### Envelope scripts

was:

`self._openoutenvelope(self.ta_info['editype'],self.ta_info['envelope'])`  
 becomes in 3.1.0:  
 `self._openoutenvelope()`  

### Route scripting

Function transform.translate is changed: parameters
startstatus,endstatus,idroute,rootidta have to be explicitly indicated
(no more defaults).

