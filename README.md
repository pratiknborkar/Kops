# Configure AWS CLI 
User must have Administrative access 
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

# Create S3 Bucket 
aws s3 mb s3://state.handsonk8s.ga

# Add you domain / cluster name is Hosted Zone using Route 53 
Make sure TTL should 60 sec or less than that for urly DNS propogation.
