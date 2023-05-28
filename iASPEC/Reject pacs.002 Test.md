

##  Reject Workflow

### 1.Test case 1, reject out

1.1. when create reject pacs.002, original message change its TRANSACTION_HDL_STS to "PENDING_FOR_RETURN_REJECT". if reject pacs.002 succed to pass approval, change its TRANSACTION_HDL_STS to "RETURN_REJECTED", if reject pacs.002 failed to pass approval, change its TRANSACTION_HDL_STS to "OUSTANDING_FOR_REVIEW"

1.2. pacs.002 exist charge

1.3. Raw Message button could click and pop out raw message

1.4. In page List of Raw Remittance Instructions:  status need to update to "SUBMITED"

1.5. check all fields are correct: handling history; User Remarks;

### 2.Test case2, reply out

2.1. inward remittance状态保持原先的OUTSTANDING_FOR_REVIEW或其他状态不变

2.2. pacs.002 doesn't exist charge

2.3. Raw Message button could click and pop out raw message

2.4. In page List of Raw Remittance Instructions:  status need to update to "SUBMITED"

2.5. check all fields are correct: handling history; User Remarks;

### 3.Test case3, receive inward 002

### 4. Host Interface Test

* succeeded to write status report pacs.002 to Host, 

* succeed to release report pacs.002 to Host

## Reject status diagram

Inward 002:   Received  -> Oustanding_For_Review -> Completed

Outward 002: NEW  ->  PENDING_ACCPETANCE -> PENDING_APPROVAL-> SUBMITTING-> COMPLETED
