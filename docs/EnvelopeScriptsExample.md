## Envelope Scripts Example Code 

bots/usersys/envelopescripts/edifact/edifact.py


This will affect all outgoing edifact documents. Add conditional logic
if needed.

    # Add some extra fields to the edifact envelope.
    # reference: http://www.stylusstudio.com/edifact/40100/UNB_.htm

    def envelopecontent(ta_info,out,*args,**kwargs):
        out.put({'BOTSID':'UNB','S002.0008': 'PARTNER1'}) # Interchange sender internal identification
        out.put({'BOTSID':'UNB','S003.0014': 'PARTNER2'}) # Interchange recipient internal identification
        out.put({'BOTSID':'UNB','0029': 'A'}) # Processing priority code
        out.put({'BOTSID':'UNB','0031': '1'}) # Acknowledgement request
