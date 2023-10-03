Test Time: 2022-11-11  16:00-19:00

Upon loading test, please be reminded to capture:
1. CPU loading & Memory consumption (e.g. use command 'vmstat 1 >> vmstat.log ').

   CPU: normally 20% -50%. Quite Often is lower than 10%

   Memory

   ​                       free            Buff                 Cache memory  

   Stress Test   160MB      127MB             6081MB

   Off-Time       447MB      128MB             4683MB

2. System through-put.

   More than 3 hundred pieces message in Redis queue waiting for processing .

3. All remittance are either STP success, or handled through Microsoft Edge using Selenium Script'. 

   All 614 outward transaction was set as "Completed". Host return status "Message in ready queue and to be sent by MERVA"

4. No duplicated submission occur.

   614 inward remittance, create 614 outward transaction and completed to submission to SWIFT. 

5. Remittance Summaries can reflect what you have tested.

   

#### hardware environment setup

Two web application servers run in separated Tomcat of same server.  Payment Processor thread pool size of single application is two.



Test Time: 2022-11-10

Result: 

Batch 1: 9:00-11:30

1.STP completed. Status: Received -> Completed   - 400 pieces.

2.Non-STP completed. Status: Received -> Outstanding_For_Review - 800 pieces



Batch 2: 16:30- 18:00

1.Non-STP handle 900 pieces. 

Status:  Outstanding_For_Review -> Completed  - 300 pieces

Status:  Outstanding_For_Review -> Acceptance - 106 pieces

Status:  Outstanding_For_Review -> Editing  -  530 pieces



Batch 3: 16:30- 18:00

No duplicate transaction.



Problem & Solution:

1.To ensure request get normal response from HOST and concurrency number  is under Host's bearable so thread pool setup began from number as small as possible, here 2.

2.A single outward transaction need at least 20s delay to get AML Result, here costing. We would divide current events into at leaset two different Thread pool, one for time cost event, another for fast-in-fast-out event. 







```
Stress Test


nohup sh jmeter.sh -n -t /opt/iaspec/apache-jmeter-5.5/bin/examples/qyk/paymentHub.jmx -l /opt/iaspec/apache-jmeter-5.5/bin/examples/qyk/report.jtl -e -o /opt/iaspec/apache-jmeter-5.5/bin/examples/qyk/result &
```

