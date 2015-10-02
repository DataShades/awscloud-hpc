HPC Instance Manager © 2015 Data Shades
Developed by shane.davis@linkdigital.com.au

The MIT License (MIT)

--------------------------------------------------------------------------
Overview

The HPC bash scripts in this repo are based on an HPC POC developed at the 
Australian National University in association with AWS, NCI, Intel and Link Digital.

There are a few prerequisites in order for the scripts to actually work. Without them
you will undoubtedly run into difficulties. As the project matures with additional
buy-in, many of the prerequisites with be accommodated within the project as
Cloud Formation and Chef scripts.

--------------------------------------------------------------------------
Prerequisites

1. Create an AMI with Slurm using http://slurm.schedmd.com/quickstart_admin.html as a guide. Tag the AMI with Name=SLURM-NODE-GM
2. Create an AWS placement group for the cluster to reside
3. Create an “AutoManage” EC2 IAM Role with an ability to provision instances (EG: PowerUserAccess), and attach an inline IAM policy as provided below
4. Create hpc-admin key pair 
5. Create security groups "Admin-Access" and "Local Traffic"
    1. Admin-Access allows external ssh
    2. Local Traffic allows all traffic from the local network. EG: 172.31.0.0/16

--------------------------------------------------------------------------
Resources

AutoManage IAM Role inline policy:
{
  "Version": "2012-10-17",
  "Statement": [
   {
      "Effect":"Allow",
      "Action":"iam:PassRole",
      "Resource":"*"
    },
    {
      "Effect":"Allow",
      "Action":"iam:ListInstanceProfiles",
      "Resource":"*"
    },
    {
      "Effect":"Allow",
      "Action":"ec2:*",
      "Resource":"*"
    }
  ]
}

