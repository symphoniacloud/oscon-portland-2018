# Create the Certificate stack (in us-east-1)

```
$ aws cloudformation create-stack \
  --region us-east-1 \
  --template-body file://certificate.yml \
  --stack-name archconf-certificate \
  --parameters ParameterKey=DomainName,ParameterValue=archconf.symphonia.io \
               ParameterKey=ValidationDomain,ParameterValue=symphonia.io
```

# Validate the certificate (via email, or DNS)

# Get the CertificateArn (from us-east-1)

```
$ aws cloudformation list-exports \
  --region us-east-1 \
  --query 'Exports[?Name==`CertificateArn`].Value' \
  --output text
```


# Update the CloudFront stack

```
$ aws cloudformation update-stack \
  --template-body file://cloudfront.yml \
  --stack-name archconf-cloudfront \
  --parameters ParameterKey=DomainName,ParameterValue=archconf.symphonia.io \
               ParameterKey=CertificateArn,ParameterValue=arn:aws:acm:us-east-1:960197636066:certificate/76127d2b-bf89-4495-b271-5c3737567cf6
```
