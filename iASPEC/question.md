1. when charge amount currency is USD, not HKD

      no usd commision amount case for now.  

2. If no commission for transaction 

   Need to submit the EXPU with no.of entry = 0

   ​    Delete the transaction 

   Need to submit the EXPU with no.of entry = 0

   

3.Remittance PACS.008 is received and its charger bearer is ‘DEBTOR’, it can still pass all the STP validation and forwarded to next instructed agent with charge bearer changed to ‘SHARE’

 The settlement amount remain unchanged under the situation?  



welcometoiaspec

welcome2iaspec

HKtz2022!

```
STPSwitchAndCutOffTimeApiHandler
 no cut time found. 不报npe
 
INGA
   query settlement  should not passed
      id=329
      id=325 
      id=328
      id=327
INDA
   compare account balance, if insufficent, not passed
   
   id=326 INDA, balance entry num =0

id=377
```

task:

给Handler取名字

DTO转成fixed Length之前先写日志

2022-08-29

1. set next instructed agent， 查哪张表 

2. code word, exception List, restricted country, cut-off time  的配置表