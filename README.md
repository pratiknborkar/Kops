# Configure AWS CLI and Create user with following access using IAM
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

# Add you domain / cluster name is Hosted Zone using Route 53 

Make sure TTL should 60 sec or less than that for urly DNS propogation.
