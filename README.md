# Deploying Amazon Connect with Infrastructure as Code

This Guidance shows you how to deploy and manage Amazon Connect using Infrastructure as Code on AWS, enabling rapid contact center setup and optimization. The solution uses AWS CloudFormation templates to automate the provisioning of Amazon Connect instances, along with integrated AWS services for a complete contact center solution. By implementing this Infrastructure as Code approach, you gain consistent, repeatable deployments while reducing manual configuration errors and streamlining your operational processes.

This Guidance is designed to be adaptable, allowing you to customize the deployment to meet your specific business requirements while maintaining operational excellence. This solution provides a foundation for delivering exceptional customer experiences at scale.

## Solution overview and architecture

![Architecture](/assets/Architecture.png)

Figure 1: Solution architecture

1.	Customer calls the Amazon Connect contact center phone number
2.	Agent gets the call on the Agent workspace and answers the call
3.	The call recordings get stored in Amazon S3 bucket
4.	For management, the performance logs are saved in Amazon CloudWatch and audit logs are saved in AWS CloudTrail
5.	S3 bucket data is encrypted using AWS KMS Key

The above solution deploys the required resources and follow the pattern:

1.	Amazon Connect Instance
2.	User stored in Amazon Connect
3.  Secrets manager to store user password
4.	Unique instance alias with Amazon Connect Agent Workspace URL
5.	Toll free number
6.	Amazon Connect Contact Flow
7.	Amazon S3 bucket for Connect call recordings.
8.	KMS keys for Connect data

To deploy this solution, you will need to have the following permissions in your AWS account:

1.	Create and manage S3 buckets
2.	Create and manage AWS Lambda resources
3.	Create and manage Amazon Connect resources

Typically, this solution should be deployed by a user with full access to your AWS environment.

1.	Click on the "Launch Stack" button to deploy the solution in your preferred region. This will be the same region that was used to deploy your Amazon Connect instance.
2.	Provide the required parameters:
    - Stack name

![Createstack](/assets/Createstack.png)

3.	Proceed with the stack creation steps.

**Note:** It will take few minutes for the stack to complete the deployment.

4.	Once the stack is deployed, get the **Password** from Secrets manager for AdminUsername and in the cloudformation **Output** tab, note the value of the **AdminUsername**, and **TollFreeNumber**. Login to the **ConnectInstanceUrl** with these credentials. 

![Stackoutput](/assets/Stackoutput.png)

5.	Navigate to the **ConnectInstanceUrl**. Log in to the application with the **AdminUsername** and **Password** collected in previous step. Make sure you allow microphone to access this URL and allow notifications if this pop up in your browser.

![Notification](/assets/Notification.png)

![Allow](/assets/Allow.png)

6.	Set agent status as **available** in the agent workspace to take the first call.

![CCP](/assets/CCP.png)

7.	Call the **TollFreeNumber** for your first call experience and **accept** the call from Agent workspace.

![Incomingcall](/assets/Incomingcall.png)

![Answeredcall](/assets/Answeredcall.png)

## Cost

Refer to amazon connect pricing: https://aws.amazon.com/connect/pricing/

## Cleanup
1.	Select the CloudFormation stack created earlier.
2.	Click on **Delete**. This will delete all the resources created as part of this CloudFormation stack.

![Deletestack](/assets/Deletestack.png)