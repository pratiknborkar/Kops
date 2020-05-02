## Configure AWS CLI and Create user
User must have Administrative access 

```bash
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "*",
            "Resource": "*"
        }
    ]
}
```

## Create S3 Bucket on my case state.handsonk8s.ga

```bash
aws s3 mb s3://state.handsonk8s.ga
```

## Install `kops` and `kubectl` 
In my case 
Installing Kops on macOS

```bash
curl -Lo kops https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-darwin-amd64
chmod +x ./kops
sudo mv ./kops /usr/local/bin/
```

Installing Kubectl on macOS

```bash
curl -Lo kubectl https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/darwin/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```
## Add you domain / cluster name is Hosted Zone using Route 53 

Make sure TTL should 60 sec or less than that for urly DNS propogation.

## Create public key

```bash
Lucifers-MacBook-Pro:.ssh lucifer$ ls
known_hosts
Lucifers-MacBook-Pro:.ssh lucifer$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/lucifer/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /Users/lucifer/.ssh/id_rsa.
Your public key has been saved in /Users/lucifer/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:ZChUKEFJAERAbmpDRsmWi0jC5YWZso8QwgKA+nYyjU0 lucifer@Lucifers-MacBook-Pro.local
The key's randomart image is:
+---[RSA 2048]----+
|^OB+=+.          |
|OX+=o  .         |
|X*+o. . o        |
|Xo  E. o         |
|o+o=    S        |
|..B.+            |
| . +             |
|                 |
|                 |
+----[SHA256]-----+
Lucifers-MacBook-Pro:.ssh lucifer$ 
Lucifers-MacBook-Pro:.ssh lucifer$ ls
id_rsa		id_rsa.pub	known_hosts
```

## Create kops cluster

```bash
kops create cluster \
--state "s3://state.handsonk8s.ga" \
--zones "us-east-1a,us-east-1b"  \
--master-count 1 \
--master-size=t2.micro \
--node-count 2 \
--node-size=t2.micro \
--name handsonk8s.ga  \
--yes
```

--state:- Your S3 bucket

--master-count:- No of Master node count here is set 1 

--master-size:- Instance type or size you can set while creating cluster

--node-count:- No of Worker node count here is set 2

--node-size:- Instance type or size you can set while creating cluster

--name:- Your Hosted zone name

## Validate kops cluster

```bash
kops validate cluster \
       --state "s3://state.handsonk8s.ga" \
       --name handsonk8s.ga
```

## Distroy kops Cluster

```bash
kops delete cluster \
       --state "s3://state.handsonk8s.ga" \
          --name handsonk8s.ga  \
       --yes
```
