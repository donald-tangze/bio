### Determine handling status by handler result priority Levels

##### 1. FIRST Received, or Auto Re-Run

* level 1: Terminate handlers execution:  

  * 1.1. Intermediary check:   Terminate,  handling status -> OUTSTANDING_FOR_REVIEW

  * 1.2. STP Switch check:  Terminate, handling status  ->  PENDING_STP

  * 1.3. Adverse weather check: Terminate, handling status  ->  PENDING_STP

  * 1.4. Cut-off time check:   Terminate, handling status -> SUSPENDED

* level 2: NON-Terminate

  > PPR would executed all handlers in order, then determine handling status based on all results and priority level.
  >
  > If all handlers passed, then transaction status -> PENDING_TRANSACTION
  >
  > If not all handler passed, then check failed handlers by below three levels:
  
  * level 2.1:  AML Check:  determine handling status by AML return code  -> OUTSTANDING_FOR_AML or PENDING_STP 
    * 2.1.1.FAILED or other unknown code -> OUTSTANDING_FOR_AML
    * 2.1.2.PENDING or NOT_FOUND -> PENDING_STP  (retry 20 times then OUTSTANDING_FOR_AML)
  * level 2.2:  NON-Terminate Other handlers: handling status ->  OUTSTANDING_FOR_REVIEW
    * 2.2.1. Future value date check: NON-Terminate,  handling status -> SUSPENDED
    * 2.2.2. All other handlers:   NON-Terminate,  handling status -> OUTSTANDING_FOR_REVIEWW
  * level 2.3:  Settlement and Balance check:  handling status ->  PENDING_STP or OUTSTANDING_FOR_REVIEW
    * 2.3.1. if and only if settlement(INGA) or balance(INDA) check failed, PPR would set status to PENDING_STP   (retry 20 times then OUTSTANDING_FOR_AML)
    * 2.3.2. if there are any else handler failed except for settlement(INGA) or balance(INDA) check, PPR would set status to OUTSTANDING_FOR_REVIEW



#####  2. Manual  Re-Run

Basically same with Received,  except four handlers would set result as RERUN_OVERWRITE (PASSED) regardless of check result is passed or not-passed.  (see underline items, which are different )These four handlers are:  a. Adverse weather check; b. Cut-off time check; c. Future value date check;  d. Holiday set check;

* level 1: Terminate handlers execution:  

  * 1.1. Intermediary check:   Terminate,  handling status -> OUTSTANDING_FOR_REVIEW

  * 1.2. STP Switch check:  Terminate, handling status  ->  PENDING_STP

  * <u>1.3. Adverse weather check: Terminate, handling status  ->  RERUN_OVERWRITE (PASSED)</u>

  * <u>1.4. Cut-off time check:   Terminate, handling status ->  RERUN_OVERWRITE (PASSED)</u>

* level 2: NON-Terminate

  > PPR would executed all handlers in order, then determine handling status based on all results and priority level.
  >
  > divide into three levels:

  * level 2.1:  AML Check:  determine handling status by AML return code  -> OUTSTANDING_FOR_AML or PENDING_STP 
    * 2.1.1.True hit -> OUTSTANDING_FOR_AML
    * 2.1.2.NOT_CLEARED or PENDING -> PENDING_STP  (retry 20 times then OUTSTANDING_FOR_AML)
    * 2.1.3.NOT_FOUND or other unknown code -> OUTSTANDING_FOR_AML
  * level 2.2:  NON-Terminate Other handlers: handling status ->  OUTSTANDING_FOR_REVIEW
    * <u>2.2.1. Future value date check: NON-Terminate,  handling status ->  RERUN_OVERWRITE (PASSED)</u>
    * <u>2.2.2. Holiday set check: NON-Terminate,  handling status ->  RERUN_OVERWRITE (PASSED)</u>
    * 2.2.3. All other handlers:   NON-Terminate,  handling status -> OUTSTANDING_FOR_REVIEWW
  * level 2.3:  Settlement and Balance check:  handling status ->  PENDING_STP or  OUTSTANDING_FOR_REVIEW
    * 2.3.1. if and only if settlement(INGA) or balance(INDA) check failed, PPR would set status to PENDING_STP   (retry 20 times then OUTSTANDING_FOR_AML)
    * 2.3.2. if there are any else handler failed except for settlement(INGA) or balance(INDA) check, PPR would set status to OUTSTANDING_FOR_REVIEW



