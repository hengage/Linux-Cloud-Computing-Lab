# Solution To Week 4, Lab 1 task

### Creating a VPC

### Steps
1. I created a VPC with a CIDR block: `aws ec2 create-vpc --cidr-block 10.0.0.0/16 --query Vpc.VpcId --output text`

2. Using the ID from my created VPC, I created a subnet with a 10.0.1.0/24 CIDR block: `aws ec2 create-subnet --vpc-id vpc-04e985bd1d514ee72 --cidr-block 10.0.1.0/24`

3. I created another subnet with the same CIDR `aws ec2 create-subnet --vpc-id vpc-2f09a348 --cidr-block 10.0.0.0/24`

4. For the next step, I made one of my subnet public. To do this,
    - I created an internet gateway: `3.aws ec2 create-internet-gateway --query InternetGateway.InternetGatewayId --output text`

    - Using the generated ID, of my internet gateway, I attached the internet gateway to my VPC: `aws ec2 attach-internet-gateway --vpc-id vpc-04e985bd1d514ee72 --internet-gateway-id igw-03f8cabae5af99322`

    - Then I created a custom route table for my VPC: `aws ec2 create-route-table --vpc-id vpc-04e985bd1d514ee72 --query RouteTable.RouteTableId --output text` 

    - After that I created a route in the route table that points all traffic (0.0.0.0/0) to the internet gateway: `aws ec2 create-route --route-table-idrtb-048077a35e78b677d --destination-cidr-block 0.0.0.0/0 --gateway-id igw-03f8cabae5af99322`

    - Next, I associated my route table with both my subnets To this, first I get the ID of my subnets with the command: `aws ec2 describe-subnets --filters "Name=vpc-id,Values=vpc-04e985bd1d514ee72" --query "Subnets[*].{ID:SubnetId,CIDR:CidrBlock}"`. With the next command, I finnaly associated my route table with one of my subnets: `aws ec2 associate-route-table  --subnet-id subnet-096f957e4e817eec4 --route-table-id rtb-048077a35e78b677d`
    