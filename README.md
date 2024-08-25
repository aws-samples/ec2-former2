## ec2-former2

[Former2](https://former2.com/) is a website that allows you to generate IaC ([Infrastructure as Code](https://docs.aws.amazon.com/whitepapers/latest/introduction-devops-aws/infrastructure-as-code.html)) templates (such as [CloudFormation](https://docs.aws.amazon.com/whitepapers/latest/introduction-devops-aws/aws-cloudformation.html), [CDK](https://docs.aws.amazon.com/whitepapers/latest/introduction-devops-aws/aws-cdk.html), Terraform, etc) from _existing_ AWS resources and is mentioned on AWS Open Source Blog ([Accelerate infrastructure as code development with open source Former2](https://aws.amazon.com/blogs/opensource/accelerate-infrastructure-as-code-development-with-open-source-former2/) and [How DNAnexus used the open source Former2 project to create infrastructure as code templates for their disaster recovery pipeline](https://aws.amazon.com/blogs/opensource/how-dnanexus-used-the-open-source-former2-project-to-create-infrastructure-as-code-templates-for-their-disaster-recovery-pipeline/)).

Some users have security concerns around entering their AWS credentials on an external website and prefer a private web instance.  However, Former2 requires [browser helper extension](https://github.com/iann0036/former2-helper) that only works with websites that has domain names 127.0.0.1, localhost, former2.com and www.former2.com. 

This CloudFormation template provisions a EC2 instance hosting former2 web codes, so that users can remote in from their browsers to generate IaC templates and download them.



## Getting started

###  Provision EC2 with CloudFormation
Download the [CloudFormation template](AmazonLinux2-former2.yaml). Login to your [CloudFormation console](https://console.aws.amazon.com/cloudformation/home#/stacks/create/template) to [create a stack](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-console-create-stack.html)


The EC2 instance is to be provisioned in a network with internet connectivity. You can select [default VPC](https://docs.aws.amazon.com/vpc/latest/userguide/default-vpc.html) and one of the [default subnets](https://docs.aws.amazon.com/vpc/latest/userguide/default-vpc.html#default-subnet). The template assumes EC2 instance in [public subnet](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Scenario1.html). To provision EC2 in [private subnet](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Scenario2.html) with internet connectivity, specify `No` for `displayPublicIP` and `assignStaticIP` Cloudformation parameter values.


### Login to EC2 instance
Once provisioned, go to **Outputs** section and use the below URL links

- `SSMSessionManager`: provides [shell access](https://aws.amazon.com/blogs/aws/new-session-manager/). From session manager terminal, set your ec2-user password with the command `sudo passwd ec2-user`
- `DCVwebConsole`: [NICE DCV](https://aws.amazon.com/hpc/dcv/) web browser client. Login as **ec2-user** and your configured password. Launch Firefox browser and install **Former 2 Helper for Mozilla Firefox**

![ec2.png](./images/ec2.png)

- `GetTokenCommand`: Copy entire string. In your NICE DCV session, open a terminal, and paste the string in to retrieve temporary IAM credentials. Use these values to enter IAM credentials at http://localhost/#section-setup-credentials


![ec2.png](./images/credentials.png)


### Using Former2
Refer to [Accelerate infrastructure as code development with open source Former2](https://aws.amazon.com/blogs/opensource/accelerate-infrastructure-as-code-development-with-open-source-former2/) blog post for Former2 usage instructions. 

## Attribution
CloudFormation template downloads Former2 web codes from [Ian Mckay](https://github.com/iann0036)'s [GitHub repo](https://github.com/iann0036/former2) which are released under [MIT license](https://github.com/iann0036/former2/blob/master/LICENSE).

## Updating web codes
Former2 is under active development. To download latest codes, login to EC2 instance and run `/home/ec2-user/update-former2` script. 

## About NICE DCV web console
[NICE DCV](https://aws.amazon.com/hpc/dcv/) supports [file transfer](https://docs.aws.amazon.com/dcv/latest/userguide/using-transfer-web.html). Usage indicates acceptance of [NICE DCV EULA](https://www.nice-dcv.com/eula.html).

![file transfer](https://docs.aws.amazon.com/images/dcv/latest/userguide/images/web-storage.png)

Native clients can be downloaded from https://download.nice-dcv.com/


## Clean Up
To remove created resources, [delete](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-console-delete-stack.html) your created CloudFormation stack


## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.
