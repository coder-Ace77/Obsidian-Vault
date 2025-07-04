
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
2. USe multifactor authentication - 2 or more auth methods. 


