

# Notes for Return/Reject

###  Return

* For completed transaction Return

  * Receive pacs.004, match original outward transaction, Debtor agent & Debtor are copied from return chain, Other info are copied from original inward

  * Receive pacs.002,  initiate pacs.004 in name of **NEXT** agent. Debtor agent & Debtor 

* instant remittance Return,  Debtor agent & Debtor is SCB

* when manually create pacs.004, **allow** to modify debtor agent & debtor
* wrongly receive pacs.004, allow to route back 

###  Reject charges

* reject handling fee.  How to show charge in pacs.002 ?   pacs.002 as payment DTO, NOT Notification DTO.

* DEBIT vostro account. (their account). Fields:  Charge Bank BIC, Charge account, charge reference

### Additional Charge report

* When receive message pacs.009, MT200, MT210, MT202 from Overseas branch or other bank, charge is not in outgoing payment, but separated charge. 

* fixed cable cost, or waive according to branch id, bank id, message type, there would be a setting configuration. 

* Operating cost is USD, while cable cost is HKD

* additional charge report is monthly,    PPR  write down GL record

  charge per transaction or per

  

Cable Cost = the count of the transaction MT200/MT202/pacs.009 from oversea SCB branch which has completed outing transactions.

Unit Cost of charge is fixed. Will hard code into report generation logic.

Unit Cost of MT200/MT202/pacs.009 or MT210 is in USD while Unit Cost of cable cost is HKD.

Fixed amount for each charge type (MT200/MT202/pacs.009 or MT210 or cable cost)

Some branches are agreed to waive MT200/MT202/pacs.009 or MT210 or cable cost.

###  Division Chief approval flow

first acceptance, transaction, payment details  forward. 

day-end  17:30  auto select 当日 payment detail list  and send email to operator.   show in FRS, functional Specification.





## PACS.004 Return

* Need to preserve the upper part of return chain from PACS.004
* The lower part of return chain preserved from PACS.008/009
* If direct return, debtor and debtor agent in return chain start from SCB
* Debtor/Creditor as agent not properly displayed
* UI allow user to edit return chain
* When return on PACS.002 rej/other message: find original payment -> create return -> edit debtor or debtor agent (possibly other fields)
* Add ***Match Payment*** function to inward PACS.004
* If received PACS.004 with incorrect agent (standard chartered -> SCB): allow route back

## PACS.002 Reject

* User: reject may involve charges
* Reject will deduct service charge separately according to transaction reference from vostro bank
* Use *additional info* to notifiy instructing agent
* User need display
  1. charge rate/amount
  2. charge settlement method (target vostro account)
* Fix charge, OBPU, GL, DW (charge collection transaction)
* 

## Others

* Every *movement/action/message* need to be included in DW