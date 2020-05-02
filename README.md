# Configure AWS CLI and Create user
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

# Create S3 Bucket on my case state.handsonk8s.ga

```bash
aws s3 mb s3://state.handsonk8s.ga
```

# Install `kops` and `kubectl` 
In my case 
Installing Kops 

# Add you domain / cluster name is Hosted Zone using Route 53 

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
Make sure TTL should 60 sec or less than that for urly DNS propogation.
