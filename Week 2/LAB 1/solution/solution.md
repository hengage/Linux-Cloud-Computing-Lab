# Solution To Week 2 Lab 1 Task

## Steps

1. As per best practices, I created an IAM user for everyday tasks.
2. I confugured my aws cloudshell using the command: `aws configure`
3. For the third step, i created and saved a key pair: `aws ec2 create-key-pair --key-name mykeypair --query 'KeyMaterial' --output text > mykeypair.pem`
4. Next i created a security group: `aws ec2 create-security-group --group-name my-schulltech-group --description "Security group for schulltech week 2, lab 1"`
5. I launched and ran an instance: `aws ec2 run-instances --image-id ami-xxxxxxx --instance-type t2.micro --key-name mykeypair security-group-ids sg-xxxxxxxxx`
