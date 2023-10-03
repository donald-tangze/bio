1. Test Case



1.1  Handler: STP & Cut-Off Time Checking



1.2  Handler:   Determine  charges and settlement amount  



1.3  Handler:   Determine  value date  

## OBPU

1.   OBPU interface                             General Ledger

iw                    save in additonal data



ow    Bank movement details               retrieve then save movement between nostro account ledger db:

​                                                                    a.  b.   (c.  d.)

​                                                                    -a -b   -c   -d

​              

|      | HOST OBPU interface                                          | DB General Ledger Table                                      |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| iw   | Bank movement details                                        | General Ledger Records                                       |
|      | generate 1 movement: if C, send to host;  if b save in additonal data | generate one gl record and one 2404031 gl record,    if C, send to host;  if B  save in additional data; |
|      |                                                              |                                                              |
| ow   | retrieve 1 movement with instructing agent. might 1 or 0     | retrieve 2 gl record with instructing agent. might 2 or 0    |
|      | generate 1 movement with instructed agent                    | generate  one gl record and one 2404031 record with instructed agent |
|      | send total 2 or 1 movenment to Host                          | then save four or two movement between nostro account ledger db |



2.   EXPU  interface                    2 General Ledger

ow    exchange  details               commision  info

ow                                                  exchange   info



1. 
2.  payment send event Type to payment processor, : OUTWARD_PAYMENT_DELETED
