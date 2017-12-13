# Get the CloudFrontDomain value

```
$ aws cloudformation list-exports \
  --query 'Exports[?Name==`CloudFrontDomain`].Value' \
  --output text
```

# Deploy the Route53 stack

```
aws cloudformation create-stack \
  --template-body file://route53.yml \
  --stack-name archconf-route53 \
  --parameters ParameterKey=DomainName,ParameterValue=archconf.symphonia.io \
               ParameterKey=CloudFrontDomain,ParameterValue=d1m7ry5mc4n7kv.cloudfront.net
```

# Update the CloudFront stack

```
aws cloudformation update-stack \
  --template-body file://cloudfront.yml \
  --stack-name archconf-cloudfront \
  --parameters ParameterKey=DomainName,ParameterValue=archconf.symphonia.io
```
