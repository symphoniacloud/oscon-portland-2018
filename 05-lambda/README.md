# Deploy the SAM bootstrap stack

```
aws cloudformation create-stack \
  --stack-name sam-bootstrap \
  --template-body file://sam-bootstrap-cfn.yml
```

# Get the S3 bucket name

```
export SAM_BUCKET=$(aws cloudformation describe-stack-resource \
  --stack-name sam-bootstrap \
  --logical-resource-id Bucket \
  --query 'StackResourceDetail.PhysicalResourceId' \
  --output text)
```

# Deploy CloudFormation stack using SAM package/deploy

Note the missing `file://` syntax. The `package` and `deploy` commands are for the Serverless Application Model, and have some slight differences from the normal CloudFormation commands.

## Package

### If you have setup Route 53 and SSL

```
aws cloudformation package \
  --s3-bucket ${SAM_BUCKET} \
  --template-file cfn.yml \
  --output-template-file cfn-packaged.yml
```

### If you have not setup Route 53 and SSL

```
aws cloudformation package \
  --s3-bucket ${SAM_BUCKET} \
  --template-file cfn-no-route53-or-ssl.yml \
  --output-template-file cfn-packaged.yml
```

## Deploy

Note that by using `deploy`, we don't have to specify unchanged parameter values.

```
aws cloudformation deploy \
  --capabilities CAPABILITY_IAM \
  --template-file cfn-packaged.yml \
  --stack-name oscon-static
```

# Upload the new "secure" content

```
aws s3 sync content s3://${OSCON_BUCKET}
```

# Visit the secure area of the site:

```
open "https://2018.oscon.symphonia.io/secure/secret.html"
```
