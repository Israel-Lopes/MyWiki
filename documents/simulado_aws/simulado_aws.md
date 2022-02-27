# Simulado AWS

### Simulado 1

(1) A develop team lead is configuration for this his team at an IT company.
Which of the following policy types onl limit permissions but cannot grant permissions (select two)?

<br />

[ ] Acess control list (ACL).

[ ] Resource-based policy.

[ ] Identiy-based policy.

[X] AWS Organization Service Control Policy (SCP).

[X] Permission boundary.

<br />

(2) The development team has just configured and attached the IAM policy needed to access AWS Billing and Cost Management for all users the Finance departament. But, the users are unable to see AWS Billing and Cost Management service in the AWS console.

What could be the reason for this issue?

[ ] Only root users has access to AWS Billing and Cost Management console.

[ ] The users might have another policy that restricts them from acessing the Billing information.

[X] You needto active IAM user access to the Billing and Cost Management console for all the users who need access.

[ ] IAM user should be created under AWS Billing and Cost Management and not under AWS account to have acess to Billing console.

<br />

(3) When running a Rolling deployment in Elastic Beanstalk environment, only thow batches completed the deployment successfully, while rest of the batches failed to deploy the updated version. Following this, the development team terminated the instances from the failed deployment.

What will be the status of these failed instances post termination?

[X] Elastic Beanstalk replace the failend instances with instances running the application version froom the most recent successful deployment.

[ ] Elastic Beanstalk will not replace the failed instances.

[ ] Elastic Beanstalk will replace the failed isntances with instances running the application version from the oldest succesfull deployment.

[ ] Elastic BEanstalk will replace the failed instances after the application version to be installed is manually chosen from AWS console.

<br />

(4) A development team whats to build an application using serveless archtecture. The team plans to use AWS Lambda function extensively this goal. Thedevelopers of the team work on different programming languages like Python, .NET and JavaScript. The team whats to model the cloud infrastructure using any of these programming languages.

Which AWS service/tool should the team use for the give use-case?

[ ] AWS Serveless Application Model(SASS).

[ ] AWS CodeDeploy.

[ ] AWS CloudFormation.

[X] AWS Cloud Development Kit (CDK).

(5) A media company has created a video streaming  application and it would like their Brazilian users to be  served by the companys brazilian servers. Other users around the globe should not be able to access the serves through DNS queries.

Which Route 53 routing policy meets this requirement?

[ ] Weighted

[X] Geolocation

[ ] Latency

[ ] Failover

<br />

(6) A development team lead is responsible for managing access for her IAM principals. At the start of the cycle, she has grated excess privileges to users to keep them motivated for trying  new  thing . She now wnats to ensure that the team has only the minimum permissions required to finish their work.

Which of the following will help her identify unused IAM roles and remove them without disrunpting any service?

[X] Access Advisor feature on IAM console.

[ ] IAM Access Analyzer

[ ] AWS Trusted Advisor

[ ] Amazon Inspector

<br />

(7) An IT company is configuring Auto Scaling fir its Amazon EC2 instances spread across different AZs and Regions.

Which of the following scenrios are NOT correct about EC2 Auto Scaling ? (select two)

[ ] For Auto Scaling groups in a VPC, the EC2 instances are lauched in subnets.

[ ] Amazon EC2 Auto Scaling attempts to distribute instances evenly between the Availabilty Zones that are enabled for your Auto Scaling group.

[ ] An Auto Scaling group can contain EC2 instances in one or more Availability Zones within the same Region.

[X] An Auto Scaling group can contain EC2 instances in only one Availability Zone of a Region

[X] Auto Scaling groups that span across multiple Regions need to be enabled for all Regions specified.

<br />

(8) You have created a Java application that uses RDS for its main data torage and ElastiCache for user session storage. The application needs to be deployed using Elastic Beanstalk and every new deployment should allow the application servers to reuse the RDS database. On the other hand, user session data stored in ElastiCache can be re-created for every deployment.

Which of the following configuration will allow you to achieve this ? (select two).

[X] RDS database defined externally and referenced through environment

[ ] ElastiCache database defined externally and referenced through environment variables.

[X] ElastiCache defined in ***.ebextensions/***

[ ] RDS database defined in ***.ebextensions/***

[ ] ElastiCache bundled with the application source code.

<br />

(9) As an AWS Certified Developer Associate, you been asked to created an AWS Elastic Beanstalk environment to handle deployment for an application that has high traffic and high availability need to  deploy the new version using Beanstalk while making sure that performace and availability are not affected.

Which of the following is the MOST optimal way to do this while keeping the solution cost-effective?

[X] Deploy using 'Rolling with additional batch' deploymnt policy

[ ] Deploy using 'Rolling' deploment policy

[ ] Deploy using 'All at once' deployment policy.

[ ] Deploy using 'Immutable' deployment policy

<br />

(10) A Developer has been entrusted with the job of securing certain S3 buckets that are shared by a large team of users. Las time, a bucket policy was chaged, the bucket was erroneously available for everyone, outside the organization too.

Which feature/service will help the developer identify similar security issues with minimum effort?

[ ] S3 Object Lock

[X] IAM Access Analyzer

[ ] Access Advisor feature on IAM console

[ ] S3 Analytics

<br />

(10) A Developer has been entrusted with the job of securing certain S3 buckets that are shared by a large team of users. Last time, a bucket policy was chaged, the bucket was erroneously available for everyone, outside the organization too.

Which feature/service will help the developer identify similar security issues with minimum effort?

[ ] S3 Object Lock

[X] IAM Access Analzer

[ ] Access Advisor feature on IAM console

[ ] Access Advisor feature on IAM console

[ ] S3 Analytics

<br />

(11) An organization has hosted its EC2 instances in two AZs. AZ1 has two instances and AZ2 has 8 instances. The Elastic Load Balancer managing the instances in the two AZs has cross-zone load balacing enabled in its configuration.

What percentage traffic will each of the instances in AZ1 receive?

[ ] 15

[ ] 25

[ ] 20

[X] 10

<br />

(12) A multi-national company has just moved to AWS Cloud and it has configured forecast-based AWS Budgets alerts for cost management. However, no alerts have been received even though the account and the budgets have been created almost three weeks ago.

[X] AWS requires approxiately 5 weeks of usage data to generate budget forecast.

[ ] Budget forecast has been created from an account that does not have enough privileges

[ ] Amazon CloudWatch could be down and hence alerts are not being sent.

[ ] Account has to be part of AWS Organizations to receive AWS Budgets alerts

<br />

(13) A developer has been asked to create an application that can be deployed across a fleet of EC2 instances The configuration must allow for full control over the deployment steps using the blue-green deployment.

Which service will help you achieve that ?

[X] CodeDeploy

[ ] CodePipeline

[ ] CodeBuild

[ ] Elastic Beanstalk

<br />

(14) A multi-national company has multiple business units with each unit having its own AWS account. The development team at the company would like to debug and trace data across account and visualize it in a centralized account.

As  Developer Associate, which of the following solutions would you suggest for the give use-case?

[ ] CloudWatch Events

[ ] CloudTrail

[X] X-Ray

[ ] VPC Flow Logs

<br />

(15) Your company has configured AWS Organizations to manage multiple AWS accounts. Within each script output the account number of the account the script was executed in.

Which Pseudo parameter will you use to get this information?

[X] AWS::Accountld

[ ] AWS::NoValue

[ ] AWS::StackName

[ ] AWS::Region

<br />

(16) An organization has offices across multiple locations and the technology team has configured an Application Load Balancer across targets in multiple Availability Zones. The team wants to analyze the incoming request for latencies and the clients IP address patterns

Which feature of the Load Balancer will help collect the required information?

[X] ALB acess logs

[ ] CloudTrail logs

[ ] CloudWatch metrics

[ ] ALB request tracing

<br />

(17) As an AWS Certifield Developer Associate, you have configured the AWS CLI on your workstation. Your default region is us-east-1 your IAM user has permissions to operate commands on services such as EC2, S3 and RDS in any region. You would like to execute a command to stop an EC2 instance in the us-east-2 region.

What of the followingis the MOST optimal solution to address this use-case?

[ ] You should create a new IAM user just for that other region.

[ ] Use boto3 dependency injection

[ ] You need to override the default region by using aws configure.

[X] Use the --region parameter

<br />


