
---

Three kinds of deployments:

1. On primises: Managed in thier own data centers. Cost of maintainance is huge.
2. Cloud: On demand delivery of IT services and resources. 
3. Hybird: Some deployment on own data centers and some on cloud.

Advantages of cloud:

1. Saves time during setup and removes unecessary and redundant tasks.
2. By removing repetitive and non differneitatng tasks one can focus on bussiness

Six major advantages:

1. Pay as you go: On primises require you to invest in data centers and hardware that may not be used. On the other hand pay as go allow you to pay only for resources that you use.
2. Economies of scale: Since many bussiness will be using the cloud solution the cost comes down to be cheaper than what you can get on your own.
3. No capacity guesses.
4. Resources are available in minutes.
5. Realize cost savings.
6. Go global in minutes.

### AWS global infra:

AWS services are divided into regions. Regions are geographic divisions created by AWS. AWS regions are named after the location where they reside. Each region has name and code.

AWS regions are independent from each other. Without explicit customer consent and auth data is not replicated from one region to other. To decide where to host consider four factors.

1. Latency: Delay between request and response - If aplication is latency sensitive choose the region close to your base. This prevents long waiting queues.
2. Prices: Due to local economy prices vary from region to region.
3. Service availabilty: Some resources are only available in only certain areas.
4. Data compliance: Companies may be required to store the customer data into some required region.

Each region is further cluster of Availability zones. Each zone consist of one or more data center which operate in discrete facilities and undisclosed locations. Note that in a region data centers are connected through high speed and low atency links.

Availability zones also hava code names and can be address by appending a letter to code name.

Any resource that one client is using may deployed either at Availability zone level or region or global level. Each service is different. By default most services are deployed at region scope level. To keep application available one must maintain high availability and resiliency. Region scopred services have resiliency built in. If deploying at availability zone level at minimum use two zones so if one zone becomes inactive you can use other one.


### Edge locations:

These are the locations where content is cached. Amazon cloudfront delivers the content through network of edge locations. when a user request content is served with cloud front, request is routed to provide lowest latency.

### Interacting with AWS:

Every action made on aws is an api call which authenticated and authorised. In aws one can make API call to services and resources through:

1. AWS management console
2. AWS cmd line (aws cli)
3. AWS SDKs

AWS CLI:  Allows you to automatically access some of aws services.

AWS SDKs : API calls to AWS can be performed by running code with programming languages. They are open source and maintained in languages like c++ , go , Java ,Python etc..

Developers commonly use AWS SDK to integrate their application code with AWS services. 

### AWS root user:

When you first login to AWS the entity is called root user it has access to all the services of that account and can be accessed by signing the email and password of account.

#### AWS root credentials:

First credentials are email and password used to create account other are access keys which allow us to make program requests from AWS cli

ACCESS key has two parts - access key ID , secret access kye
Works similar to email and password combo.

Tips:

1. Root user credentials must not be used to carry out daily work.
2. USe multifactor authentication - 2 or more auth methods. (MFA)

#### Authentication vs authorisation:

Authentication: ensures that user is who they say they are. Email/ password or ACCESS key etc.
Authorisation: What action that user can take.

##### IAM : 

Identity and access management helps to manage aws account and resources. It provides central view to both auths.

1. IAM is global.
2. Integreated by AWS services.
3. Shared access
4. MFA

An IAM user repesents a person or  service interacting with AWS. One can define user in AWS account. So one should create IAM user and then generate auth keys for that IAM user. 

An IAM user can be provided 
1. Access to AWS management console.
2. Programming access to AWS CLI and AWS API.

To access console, provide user with user name and password. For programming access AWS genereates set of access keys. When IAM user is created it gets permission at user level. But manageing large teams can be hectic. 

#### IAM groups:

Group is a collectiion of users. All users in group inherit permission of group. So we can give permission to multiple users at once. Groups can be admin , developers , security engineer etc.

Group can have many users.
Users belong to many groups.

IAM policy is set of access rules assinged to an IAM identity. When any IAM identity makes any API call AWS evaluates the policy associated with them.

Writing AWS policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::*",
        "arn:aws:s3:::*/*"
      ]
    }
  ]
}
```

Effect has two options -> allow / deny
Action -> Determines the type of action to be done.
Resource -> Type of objects that policy statement covers. * means wildcard/all.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-secure-bucket/*",
      "Condition": {
        "Bool": {
          "aws:MultiFactorAuthPresent": "true"
        }
      }
    }
  ]
}
```

#### IAM roles:

An **IAM Role** in AWS is an identity **with specific permissions** that can be assumed by **trusted entities** (like EC2 instances, Lambda functions, users from other accounts, etc.). Unlike users, **roles don't have long-term credentials** (like username/password); instead, temporary security credentials are used.

Why? Actually In practice every API call made to AWS service must be programmically signed and is authenticated. Suppose your EC2 instance wants to access the Storage then EC2 insatance will require auth keys to access storage. Ec2 will thus be assigned an IAM role. Roles are assumed programmcally and these credentails are temporary. Similarly external users can also assume IAM role. These are called federated users.

#### Basics of launching EC2

Most easy to do from AWS console. EC2 instance is a single VM that is hosted on AWS. We can either generate ssh keys and then connect to it via ssh. 

or we can provide it a script that will run when instance is launched. Finally we can access thorugh IP. 


