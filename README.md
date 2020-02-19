# CloudFormation and the New AWS CLI
CloudFormation provides a number of different ways to use the service. From the web API to language-specific SDKs to GUIs like the AWS Management Console, you choose the interface that’s right

The CloudFormation CLI  provides helpful tools that let you manage stacks from your command line. Commands like cfn-create-stack, cfn-describe-stack-resources, and cfn-delete-stack make it simple yet powerful to orchestrate and manage AWS infrastructure and apps. The new unified AWS CLI – which recently moved from Developer Preview to General Availability – replaces the original CLI and brings a ton of great new features: the new CLI includes all services in the same installation (and it’s simple to install), provides multiple outputs (from JSON to table-formatted), and gives you advanced features like command and parameter auto-completion. 

### Create a Stack
Creating a new CloudFormation stack via the original CLI involved the cfn-create-stack command. To run the stack using the new AWS CLI execute:
```sh
$aws cloudformation --profile dev-profile create-stack --stack-name csye6225demo --region us-east-1 --template-body file:///home/ananya/Downloads/cloudformation-template.json --parameters ParameterKey=VPCName,ParameterValue=dev-vpc-csye6255 ParameterKey=VPCCidrBlockParameter,ParameterValue=10.0.0.0/16 ParameterKey=Subnet1CIDRBlock,ParameterValue=10.0.0.0/25 ParameterKey=Subnet2CIDRBlock ParameterKey=Subnet2CIDRBlock,ParameterValue=10.0.1.0/25 ParameterKey=Subnet3CIDRBlock,ParameterValue=10.0.2.0/25
```


The output of that command is a JSON object with the ARN of the stack:

```sh
{
     "StackId": "arn:aws:cloudformation:us-east-1:191420594415:stack/csye6225demo1/d6f30bc0-536b-11ea-88dd-0a029b5a039d"
}
```

### Describe Stack Resources

CloudFormation makes it straightforward, repeatable, and predictable to create a complex environment in AWS, but once a stack is up and running CloudFormation also provides an API to locate individual resources in the stack, serving as a ‘resource catalog’ of sorts. To get detailed information about the resource call the "describe-stack-resource API:"

```sh
aws cloudformation describe-stack-resource --stack-name csye6225demo 
--logical-resource-id DBInstance
```


### Delete the stack
The following delete-stack-instances example deletes instances of a stack set in the region and terminates the stacks.

```sh
$ aws cloudformation --profile dev-profile delete-stack --stack-name csye6225demo --region us-east-1 
```
