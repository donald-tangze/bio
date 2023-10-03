![image-20220126122552516](https://tva1.sinaimg.cn/large/e6c9d24egy1h39x2fs6u5j20kj087q3m.jpg)

Cloud service

cloud operation,  continuous operation:  zero downtime

tool and tech: Redundancy  冗余

* cloud management platform:    provisioning. Automated process
* AIOPS
* Metric and Monitoring system:  cloud monitoring

 

AMS account  

bjtangze@gmail.com    HKtz2023!

donald.tangze@outlook.com HKtz2022!            

Amazon  account       

##  2.AWS tutorial

[Connect to your Linux instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connect-to-linux-instance.html#connection-prereqs-private-key)

* [Get information about your instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connect-to-linux-instance.html#connection-prereqs-get-info-about-instance)
* [Locate the private key and set permissions](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connect-to-linux-instance.html#connection-prereqs-private-key)





```shell
// SSH connect to EC2
ssh -i C:/Users/donal/.ssh/mac_id_ed25519 ec2-user@ec2-3-36-131-171.ap-northeast-2.compute.amazonaws.com

//   upload file 
scp -i C:/Users/donal/.ssh/mac_id_ed25519 'C:/Users/donal/OneDrive/Workspace/Spring/Spring guides 2023/my-rest-service/target/my-rest-service-0.0.1-SNAPSHOT.jar'   ec2-user@ec2-3-36-131-171.ap-northeast-2.compute.amazonaws.com:/home/ec2-user/spring-service/

curl 3.36.131.171:8080/greeting

IAM  https://733429469646.signin.aws.amazon.com/console
User name: donald           Console password:  VoNzl%2!

nohup java -jar /home/ec2-user/spring-service/my-rest-service-0.0.1-SNAPSHOT.jar
```

AWS components

* EC2  (Security Group)    SSH connection

* ECS  Elastic Container Service

* Amplify

* S3

* [CodeCommit]() (Equivalent to Github, code public repository)

* [CodeBuild] (https://docs.aws.amazon.com/codebuild/latest/userguide/concepts.html)

  > [Build specification reference for CodeBuild - AWS CodeBuild (amazon.com)](https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html)

* CodeDeploy

  > [CodeDeploy AppSpec File reference](https://docs.aws.amazon.com/codedeploy/latest/userguide/reference-appspec-file.html)
  >
  > [Install the CodeDeploy agent for Amazon Linux or RHEL](https://docs.aws.amazon.com/codedeploy/latest/userguide/codedeploy-agent-operations-install-linux.html)
  >
  > | Asia Pacific (Seoul) | aws-codedeploy-ap-northeast-2 | ap-northeast-2 |
  > | -------------------- | ----------------------------- | -------------- |
  >
  > ```
  > wget https://aws-codedeploy-ap-northeast-2.s3.ap-northeast-2.amazonaws.com/latest/install
  > ```





* CodePipline

* 
