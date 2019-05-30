# AWS-EC2-Jenkins-Automation
Author: shadyshrew

Uses Ansible to provision a EC2 instance and installs Jenkins on the provisioned instance.

# Prerequisites

## Requirements: 
1) python 2.7
2) ansible 2.6.5
3) boto and boto3
      - nose
      - tornado
4) AWS CLI

## Steps (Assuming you have python): 
```
easy_install pip
pip install ansible==2.6.5
pip install nose
pip install tornado
pip install boto
pip install boto3
```

## Install and Configure AWS CLI: 
1) `curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip"`
2) `unzip awscli-bundle.zip`
3) `sudo ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws`
3) Make changes to the following files
      a) `~/.aws/config`
      b) `~/.aws/credentials`

## Changes to `~/.aws/config`
  ```
  [default]
  role_arn = arn:aws:iam::<account_id_number>:role/<role_name>
  output = json
  region = <region name> ex. us-east-1
  source_profile = <aws username>

  [profile <aws username>]
  output = json
  region = <region name> ex. us-east-1

  [profile <child profile>]
  role_arn = arn:aws:iam::<account_id_number>:role/<role_name>
  output = json
  region = <region name> ex. us-east-1
  source_profile = <aws username>
  ```
## Changes to `~/.aws/credentials` 

```
[default]

[<child profile>]  #Child profile is yours to name!
aws_access_key_id = <access key>
aws_secret_access_key = <secret key>

[<aws username>]
aws_access_key_id = <access key>
aws_secret_access_key = <secret key>
```

## AWS EC2 Prerequistes
1) Create a keypair and download it from AWS EC2, you will only be able to download this keypair once.
2) Move your keypair to `~/.ssh`
3) Change permissions of the keypair to 400
      `chmod 400 ~/.ssh/<keypair name>.pem`

# Run the code
`ansible-playbook AnsibleAutomate.yml`

## Copy and paste the URL in your browser to access the Jenkins Server
