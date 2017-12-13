# Deploy the CloudFront stack

```
aws cloudformation create-stack \
  --template-body file://cloudfront.yml \
  --stack-name archconf-cloudfront
```

# Get the distribution domain name

```
aws cloudformation list-exports \
  --query 'Exports[?Name==`CloudFrontDomain`].Value' \
  --output text
```

# Visit the domain

```
open "..."
```

# Check out the latency

```
curl -o /dev/null -s -w "%{time_total}\n" ...
```
