# Update the CloudFormation stack

```
aws cloudformation update-stack \
  --template-body file://cfn.yml \
  --stack-name oscon-static
```

# Get the CloudFront distribution id and domain name

```
export OSCON_CLOUDFRONT_ID=$(aws cloudformation describe-stack-resource \
  --stack-name oscon-static \
  --logical-resource-id CloudFrontDistribution \
  --query 'StackResourceDetail.PhysicalResourceId' \
  --output text)

export OSCON_CLOUDFRONT_DOMAIN=$(aws cloudfront get-distribution \
  --id ${OSCON_CLOUDFRONT_ID} \
  --query 'Distribution.DomainName' \
  --output text)
```

# Visit the domain

```
open "http://${OSCON_CLOUDFRONT_DOMAIN}"
```

# Check out the latency

```
curl -o /dev/null -s -w "%{time_total}\n" "http://${OSCON_CLOUDFRONT_DOMAIN}"
```
