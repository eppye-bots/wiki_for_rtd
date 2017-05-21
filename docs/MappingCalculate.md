## Calculations and counting in mapping 

Sometimes it is needed to do calculations in mappings.  
Realize that the get() functions always return strings, so these
strings need to be converted.  
Always convert to python's decimals, this is the **only** way to avoid
rounding errors. More details: [pythons decimal
documentation](http://docs.python.org/2/library/decimal.html)

### Example calculation

```python
import decimal

def main(inn,out):
    TOTAL_AMOUNT = decimal.Decimal('0')         #initialize total amount
    for lin inn.getloop({'BOTSID':'UNH'},{'BOTSID':'LIN'}):
        amount = lin.get({'BOTSID':'LIN'},{'BOTSID':'QTY','1234':None}) 
        TOTAL_AMOUNT += decimal.Decimal(amount)   #add amount to TOTAL_AMOUNT
      
    #convert TOTAL_AMOUNT back to string, indicating the number of decimals to be used (precision)      
    total_amount = TOTAL_AMOUNT.quantize(decimal.Decimal('1.00'))   #2 decimals precision
```

Bots version 3.1 has a new method getdecimal(); code above can now be:

```python
import decimal

def main(inn,out):
    TOTAL_AMOUNT = decimal.Decimal('0')         #initialize total amount
    for lin inn.getloop({'BOTSID':'UNH'},{'BOTSID':'LIN'}):
        TOTAL_AMOUNT += lin.getdecimal({'BOTSID':'LIN'},{'BOTSID':'QTY','1234':None})   #add amount to TOTAL_AMOUNT
  
    #convert TOTAL_AMOUNT back to string, indicating the number of decimals to be used (precision)      
    total_amount = TOTAL_AMOUNT.quantize(decimal.Decimal('1.00'))   #2 decimals precision
```

Note: the example above could be done using function getcountsum(), see
below. The recipe above gives you detailed control over the
calculation.



### getcount()

returns the number of records in the tree or node.  
typically used for UNT-count of segments.

```python
out.getcount()
#returns the numbers of records in outmessage.
```

### getcountoccurrences(mpath)

returns the number of records selected by mpath.  
typically used to count number of LIN segments.

```python
out.getcountoccurrences({'BOTSID':'UNH'},{'BOTSID':'LIN'}) 
#returns the numbers of LIN-records.
```

### getcountsum(mpath)

counts the totals value as selected by mpath.  
typically used to count total number of ordered articles.

```python
out.getcountsum({'BOTSID':'UNH'},{'BOTSID':'LIN'},{'BOTSID':'QTY','C186.6063':'12','C186.6060':None}) 
#returns total number of ordered articles.
```
