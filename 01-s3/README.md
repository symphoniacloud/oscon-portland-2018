# Deploy the stack

```
aws cloudformation create-stack \
  --template-body file://cfn.yml \
  --stack-name oscon-phase-1
```

# Get the bucket name

```
export OSCON_BUCKET=$(aws cloudformation list-stack-resources \
  --stack-name oscon-phase-1 \
  --query 'StackResourceSummaries[?LogicalResourceId==`Bucket`].PhysicalResourceId' \
  --output text)
```

# Visit the bucket URL, observe 404

```
open "http://${OSCON_BUCKET}.s3-website-us-east-1.amazonaws.com"
```

# Upload some content!

```
aws s3 sync content s3://${OSCON_BUCKET}
```

# Check out the latency

```
curl -o /dev/null -s -w "%{time_total}\n" "http://${OSCON_BUCKET}.s3-website-us-east-1.amazonaws.com"
```
