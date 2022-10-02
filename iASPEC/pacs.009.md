####  Part1: pacs.008 

keep same with our code implement



#### Part2: pacs.008[COVE] + pacs.009.cov

when pacs.008 has COV settlement method, check if  settlement method = INDA and NOSTRO account exist in DB by reimbursement agent bic.

* if settlement Method = "INDA", set result = NOT_PASSED and handling_status = "outstanding for review"
* if settlement Method = "INGA" and don't exist NOSTRO account, set result = NOT_PASSED and handling_status = "outstanding for review"
* if settlement Method = "INGA" and exist NOSTRO account, check if statement received, 
  * if inward passed all handlers, then begin new outward transaction process as usual
  * if don't passed handlers, set result = NOT_PASSED

Responsibility of inward BankRelatedAccountHandler.

> pacs.008[cov]   need normal settlement and send out a pacs.008 as usual, inward settlement happen between us and reimbursement agent.  Outward agent is determine by intermediary agent, outward settlement happen between us and instructed agent.
>
> pacs.009.cov  creditor agent and instructed agent are all us SCB,  no need to handle

#### Part3: pacs.009/ pacs.009.COV

##### inward process

do settlement as usual.   Responsibility of inward BankRelatedAccountHandler and SettlementAndBalanceHandler

##### outward process

find if next instructed  agent's NOSTRO account exist,

* if exist, set ow settlement Method = "INDA" and continue outward transaction process,  outward message type keep same as inward message;
* if don't exist, set result = NOT_PASSED, and handling_status = "outstanding for review", won't create outward transaction

Responsibility of inward DetermineOutwardMethodHandler

> inward pacs.009, outward pacs.009, need settlement,  proceed as usual,  inward settlement happen between us and instructing agent, outward settlement happen between us and instructed agent
>
> inward pacs.009.cov, outward pacs.009.cov, need settlement,  proceed as usual
>
> 