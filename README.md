# infrastructure

- Two profiles dev and prod are created using 'aws configure' command in AWS CLI.
- Using network.json we lay down the network stack in the cloud. 
- Network stacks consists of Virtual Private Cloud (VPC), 3 subnets are attached in this VPC, Internet Gateway is attached to VPC. A public route table is created and all subnets created above are atached to the route table.4

- To create this stack
- aws cloudformation create-stack \
  --stack-name assignment-5 \
  --region us-east-1 \
  --profile dev \
  --parameters \
  ParameterKey=InstanceTypeParameter,ParameterValue=t2.micro \
  ParameterKey=VPCCidrBlock,ParameterValue=10.0.0.0/16 \
  ParameterKey=VPCName,ParameterValue=VPC \
  ParameterKey=SSHKeyPair,ParameterValue=aws \
  ParameterKey=AvailabilityZone1,ParameterValue=us-east-1a \
  ParameterKey=AvailabilityZone2,ParameterValue=us-east-1e \
  ParameterKey=AvailabilityZone3,ParameterValue=us-east-1c \
  ParameterKey=PublicSubnetCidrBlock1,ParameterValue=10.0.1.0/24 \
  ParameterKey=PublicSubnetCidrBlock2,ParameterValue=10.0.2.0/24 \
  ParameterKey=PublicSubnetCidrBlock3,ParameterValue=10.0.3.0/24 \
  --template-body file://network.json

- To delete this stack :
aws cloudformation delete-stack --region us-east-1 --stack-name stackname

- To import certificate :
aws acm import-certificate --profile prod --certificate file://certificate_crt.pem --certificate-chain file://certificate_bundle.pem --private-key file://certificate_key.pem