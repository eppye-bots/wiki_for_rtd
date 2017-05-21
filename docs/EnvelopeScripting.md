## Envelope scripting

You can use an envelopescript to do custom enveloping for edifact, 
x12, tradacoms, xml. Exit points that can be used: 

1. 	ta\_infocontent(ta\_info) \* at start of enveloping
	process. ta\_info contains the values that are used to write the
	envelope; you can change these values. 
1.	envelopecontent(ta\_info,out) \* after bots has built the envelope
	tree you can make changes to the envelope tree by using put(), change()
	etc.
    
Functions should be in
*bots/usersys/envelopescripts/`<editype>`/`<editype>`.py*, eg:

-   *bots/usersys/envelopescripts/edifact/edifact.py*
-   *bots/usersys/envelopescripts/x12/x12.py*


### Examples


#### Example 1

Note that this affects all outgoing edifact documents. Add conditional
logic if needed.  
In file *bots/usersys/envelopescripts/edifact/edifact.py*:

    def envelopecontent(ta_info,out,*args,**kwargs):
        ''' Add extra fields to the edifact envelope.'''
        out.put({'BOTSID':'UNB','S002.0008': 'PARTNER1'}) #Interchange sender internal identification
        out.put({'BOTSID':'UNB','S003.0014': 'PARTNER2'}) #Interchange recipient internal identification
        out.put({'BOTSID':'UNB','0029': 'A'})             #Processing priority code
        out.put({'BOTSID':'UNB','0032': 'EANCOM'})        #Interchange agreement identifier


#### Example 2

In file *bots/usersys/envelopescripts/edifact/edifact.py*:

    def ta_infocontent(ta_info,*args,**kwargs):
        ''' function is called before envelope tree is made.
            values in ta_info will be used to create envelope.
        '''
        if ta_info['topartner'] == '1111111111111':
            ta_info['topartner'] = 'XXXXXXXXXXXXXXXXX'
            ta_info['UNB.S003.0014'] = '012345'


#### Example 3

In file *bots/usersys/envelopescripts/edifact/edifact.py*:

    def envelopecontent(ta_info,out,*args,**kwargs):
        ''' function is called after envelope tree is made, but not written yet.
            manipulate envelope tree itself.
        '''
        if ta_info['topartner'] == '1111111111111':
            out.change(where=({'BOTSID':'UNB'},),change={'S003.0010': 'XXXXXXXXXXXXXXXXX'}) #field S003.0010 (receiver) is written to envelope tree
            out.put({'BOTSID':'UNB','S003.0014': '012345'}) #field S003.0014 is written to envelope tree
            ta_info['topartner'] = 'XXXXXXXXXXXXXXXXX'      #takes only care of changing the partnerID in bots interface (does not change envelope itself)
