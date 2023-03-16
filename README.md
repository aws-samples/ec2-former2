## ec2-former2

[Former2](https://former2.com/) is a website that allows you to generate IaC (CloudFormation, Terraform, CDK, etc) scripts from _existing_ AWS resources and is mentioned on AWS blog ([Accelerate infrastructure as code development with open source Former2](https://aws.amazon.com/blogs/opensource/accelerate-infrastructure-as-code-development-with-open-source-former2/) and [How DNAnexus used the open source Former2 project to create infrastructure as code templates for their disaster recovery pipeline](https://aws.amazon.com/blogs/opensource/how-dnanexus-used-the-open-source-former2-project-to-create-infrastructure-as-code-templates-for-their-disaster-recovery-pipeline/)).

Some users have security concerns around entering their AWS credentials on an external website and prefer a private instance.  However, Former2 requires browser extension that only works with websites that has domain names localhost, former2.com and www.former2.com. 

This CloudFormation template provisions a EC2 instance hosting former2 web codes, so that users can remote in from their browsers to use and download the generated IaC file. 



## Getting started

Download the [CloudFormation template](template.yaml) and provision it in your AWS console. 
Once provisioned, go to Outputs section.

![outputs.png](./images/outputs.png)

Use the `SSMSessionManager` link value to change ec2-user password and `RemoteWebConsole` link value to login to graphical desktop login in your browser. 



![ec2.png](./images/ec2.png)

Refer to [Accelerate infrastructure as code development with open source Former2](https://aws.amazon.com/blogs/opensource/accelerate-infrastructure-as-code-development-with-open-source-former2/) blog post for Former2 usage instructions. 

## About remote web console
Remote web access is provided by [NICE DCV](https://aws.amazon.com/hpc/dcv/) server, and supports [file transfer](https://docs.aws.amazon.com/dcv/latest/userguide/using-transfer-web.html). Native clients can be downloaded from https://download.nice-dcv.com/

![file transfer](https://docs.aws.amazon.com/images/dcv/latest/userguide/images/web-storage.png)


## Attribution
CloudFormation template downloads Former2 web codes from https://github.com/iann0036/former2 which are released under [MIT license](https://github.com/iann0036/former2/blob/master/LICENSE).


## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.
