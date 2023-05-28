1. Redis Interface, reply-required=true, set receive-timeout="30"

   ```
   search 	int-redis:queue-inbound-gateway in ApplicationContext-redis-int.xml
   
   two places:
   1.paymentService invoke SMXA Service
   2.paymentProcessor invoke SMXA Service
   ```

https://gitlab.hk1.iaspec.com/payment-hub/rtmg/-/merge_requests



Phase 2:

BRANCH:  Redis-queue 

https://gitlab.hk1.iaspec.com/payment-hub/payment-hub/-/merge_requests/14

https://gitlab.hk1.iaspec.com/payment-hub/rtmg/-/merge_requests/4



search 	int-redis:queue-inbound-gateway in all ApplicationContext-redis-int.xml

Six places:
1.paymentService invoke SMXA Service

2.paymentProcessor invoke SMXA Service

3.paymentService invoke SMTA Service

4.paymentProcessor invoke SMTA Service

5.paymentService invoke CMXA Service

6.paymentProcessor invoke CMXA Service

