# Solution To Week 4, Lab 1 task

### Creating a VPC

### Steps
1. I repeated the steps from Lab 1
2. I modified the public IP of my subnet to automatically recieve a public address when an instance is launched into it: `aws ec2 modify-subnet-attribute --subnet-id subnet-02c530d0309d73a00 --map-public-ip-on-launch`
3. I created a key pair and a security group
4. For the next step, I allowed SSh acess from anywhere with Tcp port 22 and 80: `authorize-security-group-ingress --group-id sg-032c0f0ba63905fa8 --protocol tcp --port 22 --cidr 0.0.0.0/0`, `authorize-security-group-ingress --group-id sg-032c0f0ba63905fa8 --protocol tcp --port 80 --cidr 0.0.0.0/0`
5. Using my security group Id, keypair and AMI image ID, I launched my instance into my public subnet: `aws ec2 run-instances --image-id ami-0d92ae3e9abaeaccc --count 1 --instance-type t2.micro --key-name schulltechkeypair --security-group-ids sg-032c0f0ba63905fa8 --subnet-id subnet-02c530d0309d73a00`
6. I also associated an elastic IP address to my instance.