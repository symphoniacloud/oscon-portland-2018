# Deploy the stack

```
aws cloudformation create-stack \
  --template-body file://s3.yml \
  --stack-name archconf-s3
```

# Get the bucket URL

```
aws cloudformation list-exports \
  --query 'Exports[?Name==`BucketUrl`].Value' \
   --output text
```

# Visit the bucket URL, observe 404

```
open "..."
```

# Upload some content!

```
aws s3 sync content s3://...
```

# Check out the latency

```
curl -o /dev/null -s -w "%{time_total}\n" ...
```
