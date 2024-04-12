# cloudformation in aws:

**Cloudformation**:AWS CloudFormation is a service that helps you model and set up your AWS resources so that you can spend less time managing those resources and more time focusing on your applications that run in AWS. You create a template that describes all the AWS resources that you want (like Amazon EC2 instances or Amazon RDS DB instances), and CloudFormation takes care of provisioning and configuring those resources for you. You don't need to individually create and configure AWS resources and figure out what's dependent on what; CloudFormation handles that
### What does cloud formation do?
1.**Simplify infrastructure management**: For a scalable web application that also includes a backend database, you might use an Auto Scaling group, an Elastic Load Balancing load balancer, and an Amazon Relational Database Service database instance. You might use each individual service to provision these resources and after you create the resources, you would have to configure them to work together. All these tasks can add complexity and time before you even get your application up and running.

Instead, you can create a CloudFormation template or modify an existing one. A template describes all your resources and their properties. When you use that template to create a CloudFormation stack, CloudFormation provisions the Auto Scaling group, load balancer, and database for you. After the stack has been successfully created, your AWS resources are up and running. You can delete the stack just as easily, which deletes all the resources in the stack. By using CloudFormation, you easily manage a collection of resources as a single unit.

2.**Quickly replicate your infrastructure**: If your application requires additional availability, you might replicate it in multiple regions so that if one region becomes unavailable, your users can still use your application in other regions. The challenge in replicating your application is that it also requires you to replicate your resources. Not only do you need to record all the resources that your application requires, but you must also provision and configure those resources in each region.

Reuse your CloudFormation template to create your resources in a consistent and repeatable manner. To reuse your template, describe your resources once and then provision the same resources over and over in multiple regions.

3.**Easily control and track changes to your infrastructure**: In some cases, you might have underlying resources that you want to upgrade incrementally. For example, you might change to a higher-performing instance type in your Auto Scaling launch configuration so that you can reduce the maximum number of instances in your Auto Scaling group. If problems occur after you complete the update, you might need to roll back your infrastructure to the original settings. To do this manually, you not only have to remember which resources were changed, but you also have to know what the original settings were.

When you provision your infrastructure with CloudFormation, the CloudFormation template describes exactly what resources are provisioned and their settings. Because these templates are text files, you simply track differences in your templates to track changes to your infrastructure, similar to the way developers control revisions to source code. For example, you can use a version control system with your templates so that you know exactly what changes were made, who made them, and when. If at any point you need to reverse changes to your infrastructure, you can use a previous version of your template.

### AWS CloudFormation concepts:

**Templates**:A CloudFormation template is a JSON or YAML formatted text file. You can save these files with any extension, such as .json, .yaml, .template, or .txt. CloudFormation uses these templates as blueprints for building your AWS resources. For example, in a template, you can describe an Amazon EC2 instance, such as the instance type, the AMI ID, block device mappings, and its Amazon EC2 key pair name. Whenever you create a stack, you also specify a template that CloudFormation uses to create whatever you described in the template.

For example, if you created a stack with the following template, CloudFormation provisions an instance with an ami-0ff8a91507f77f867 AMI ID, t2.micro instance type, test key key pair name, and an Amazon EBS volume.
```sh
AWSTemplateFormatVersion: 2010-09-09
Description: A sample template
Resources:
  MyEC2Instance:
    Type: 'AWS::EC2::Instance'
    Properties:
      ImageId: ami-0ff8a91507f77f867
      InstanceType: t2.micro
      KeyName: testkey
      BlockDeviceMappings:
        - DeviceName: /dev/sdm
          Ebs:
            VolumeType: io1
            Iops: 200
            DeleteOnTermination: false
            VolumeSize: 20
 ```
**stacks**: When you use CloudFormation, you manage related resources as a single unit called a stack. You create, update, and delete a collection of resources by creating, updating, and deleting stacks. All the resources in a stack are defined by the stack's CloudFormation template. Suppose you created a template that includes an Auto Scaling group, Elastic Load Balancing load balancer, and an Amazon Relational Database Service (Amazon RDS) database instance. To create those resources, you create a stack by submitting the template that you created, and CloudFormation provisions all those resources for you. You can work with stacks by using the CloudFormation console, API, or AWS CLI.
### How does AWS CloudFormation work?

When creating a stack, AWS CloudFormation makes underlying service calls to AWS to provision and configure your resources. CloudFormation can only perform actions that you have permission to do. For example, to create EC2 instances by using CloudFormation, you need permissions to create instances. You'll need similar permissions to terminate instances when you delete stacks with instances. You use AWS Identity and Access Management (IAM) to manage permissions.

The calls that CloudFormation makes are all declared by your template. For example, suppose you have a template that describes an EC2 instance with a t2.micro instance type. When you use that template to create a stack, CloudFormation calls the Amazon EC2 create instance API and specifies the instance type as t2.micro. The following diagram summarizes the CloudFormation workflow for creating stacks.

Use the AWS CloudFormation Designer or your own text editor to create or modify a CloudFormation template in JSON or YAML format. You can also choose to use a provided template. The CloudFormation template describes the resources you want and their settings. For example, suppose you want to create an EC2 instance. Your template can declare an Amazon EC2 instance and describe its properties, as shown in the following example:

Example YAML
```sh
AWSTemplateFormatVersion: 2010-09-09
Description: A simple EC2 instance
Resources:
  MyEC2Instance:
    Type: 'AWS::EC2::Instance'
    Properties:
      ImageId: ami-0ff8a91507f77f867
      InstanceType: t2.micro
```
### When do you use the cloud formation template?  When do you use AWS CLI?

CloudFormation (CFT) and AWS CLI are both tools used in AWS, but for different purposes and scenarios:

1. **AWS CloudFormation (CFT)**:
   - **Purpose**: CloudFormation is used for infrastructure as code (IaC) to automate the creation, update, and deletion of AWS resources.
   - **When to use**: You would use CloudFormation when you want to define your AWS infrastructure in a template (written in JSON or YAML) and provision it in a repeatable and predictable manner. It's especially useful for managing complex, multi-resource AWS environments.

2. **AWS Command Line Interface (AWS CLI)**:
   - **Purpose**: AWS CLI is a unified tool to manage your AWS services from the command line.
   - **When to use**: You would use AWS CLI when you need to perform ad-hoc tasks, automate repetitive tasks, or integrate AWS services with scripts or other automation tools. It's also useful for managing AWS resources that are not yet supported by CloudFormation.

In summary, use CloudFormation for managing infrastructure as code and AWS CLI for interacting with AWS services from the command line for various tasks.

### What is the difference between Terraform and cloud formation templates?
Terraform and AWS CloudFormation are both infrastructure as code (IaC) tools used for defining and provisioning infrastructure in a cloud environment, but they have some key differences:

1. **Provider Support**:
   - **Terraform**: Terraform supports multiple cloud providers (AWS, Azure, Google Cloud, etc.) and even some non-cloud providers (like Kubernetes, GitHub, etc.), allowing you to manage a heterogeneous environment with a single tool.
   - **AWS CloudFormation**: CloudFormation is specific to AWS and is tightly integrated with AWS services, providing a seamless experience for AWS-specific infrastructure provisioning.

2. **Configuration Language**:
   - **Terraform**: Terraform uses its own declarative language called HashiCorp Configuration Language (HCL), which is similar to JSON but with more readability and flexibility.
   - **AWS CloudFormation**: CloudFormation uses JSON or YAML templates to define the infrastructure, which can be less expressive and more verbose compared to HCL.

3. **Resource Management**:
   - **Terraform**: Terraform manages resources using a state file, which keeps track of the current state of the infrastructure and allows for easy updates and modifications.
   - **AWS CloudFormation**: CloudFormation also maintains a state of the provisioned resources but manages it internally, without exposing it to users. Updates and modifications are handled through stack updates.

4. **Resource Drift Detection**:
   - **Terraform**: Terraform can detect and manage resource drift, i.e., differences between the desired state (defined in the configuration) and the actual state of the infrastructure, allowing you to reconcile them.
   - **AWS CloudFormation**: CloudFormation can detect drift but does not automatically correct it; you need to manually update the stack to bring it back to the desired state.

5. **Community and Ecosystem**:
   - **Terraform**: Terraform has a large and active community with many third-party providers and modules available, making it easier to reuse and share infrastructure configurations.
   - **AWS CloudFormation**: While CloudFormation has a strong integration with AWS services, its community and ecosystem are more limited compared to Terraform.

In summary, Terraform is more flexible and supports multiple cloud providers, while CloudFormation is tightly integrated with AWS and provides a seamless experience for managing AWS-specific infrastructure. The choice between them depends on your specific requirements and the complexity of your infrastructure.

### What is drift detection in cft?

Drift detection in AWS CloudFormation is a feature that allows you to detect differences between the expected configuration of your AWS resources, as defined in your CloudFormation template, and the actual configuration of those resources in your AWS account. 

When you create or update a CloudFormation stack, CloudFormation creates a stack drift detection status that indicates whether any resources in the stack differ from the stack template. You can then use the CloudFormation console, AWS CLI, or SDKs to detect drift and view detailed information about the differences.

Drift detection is useful for ensuring that the actual state of your AWS resources matches your expected configuration. If drift is detected, you can take action to reconcile the differences, such as updating the stack to bring it back into compliance with the template or updating the template to reflect the current state of the resources.

# AWS-Codecommit

### What is AWS CodeCommit?

AWS CodeCommit is a version control service hosted by Amazon Web Services that you can use to privately store and manage assets (such as documents, source code, and binary files) in the cloud.

## Introducing CodeCommit

CodeCommit is a secure, highly scalable, managed source control service that hosts private Git repositories. CodeCommit eliminates the need for you to manage your own source control system or worry about scaling its infrastructure. You can use CodeCommit to store anything from code to binaries. It supports the standard functionality of Git, so it works seamlessly with your existing Git-based tools.

## With CodeCommit, you can:

**Benefit from a fully managed service hosted by AWS**. CodeCommit provides high service availability and durability and eliminates the administrative overhead of managing your own hardware and software. There is no hardware to provision and scale and no server software to install, configure, and update.

**Store your code securely**. CodeCommit repositories are encrypted at rest as well as in transit.

**Work collaboratively on code**. CodeCommit repositories support pull requests, where users can review and comment on each other's code changes before merging them to branches; notifications that automatically send emails to users about pull requests and comments; and more.

**Easily scale your version control projects**. CodeCommit repositories can scale up to meet your development needs. The service can handle repositories with large numbers of files or branches, large file sizes, and lengthy revision histories.

**Store anything, anytime**. CodeCommit has no limit on the size of your repositories or on the file types you can store.

**Integrate with other AWS and third-party services**. CodeCommit keeps your repositories close to your other production resources in the AWS Cloud, which helps increase the speed and frequency of your development lifecycle. It is integrated with IAM and can be used with other AWS services and in parallel with other repositories. For more information, see Product and service integrations with AWS CodeCommit.

**Easily migrate files from other remote repositories**. You can migrate to CodeCommit from any Git-based repository.

**Use the Git tools you already know**. CodeCommit supports Git commands as well as its own AWS CLI commands and APIs.

