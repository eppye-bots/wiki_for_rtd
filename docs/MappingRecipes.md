## Mapping recipes

### multiple messages in an edi-file, not split up

(a grammar without nextmessage)

-   Using inn.get() gives an error: that "root" of incoming message is
    empty, etc.
-   You start the mapping script with getloop(); and do get() with
    results of getloop()


### Csv messages consisting of only one record type

use nextmessageblock() to separate the messages

see plugin ...

