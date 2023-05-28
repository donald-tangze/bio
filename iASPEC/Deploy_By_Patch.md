# Patch-deploy

##  Deploy on 20230430





# patch 20230314 Payment Hub SMXA

# Purpose
  - UAT#10 - Slow response after confirm submit transaction. 


# Applies To
  - SMXA

# How to apply

1) Execute apply_patch.sh

    * sh apply_patch -prepare <destination dir>  result: generate three scripts:1.apply.sh 2.backup.sh 3.rollback.sh
    * execute 2.backup.sh, 

    * then execute 1.apply.sh

2) (if exists) do according to Manual.txt

3) Restart listed modules
    operation-desk



## install PPR in production 

1.Tomcat server.

2.database, redis, ibm mq,

3.Configuration properties,  jms.properties, redis.properties

4.cronb Scheduler setup
