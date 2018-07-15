# Deploy the stack

```
aws cloudformation create-stack \
  --template-body file://cfn.yml \
  --stack-name oscon-static
```

# Get the bucket name

```
export OSCON_BUCKET=$(aws cloudformation describe-stack-resource \
  --stack-name oscon-static \
  --logical-resource-id Bucket \
  --query 'StackResourceDetail.PhysicalResourceId' \
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
