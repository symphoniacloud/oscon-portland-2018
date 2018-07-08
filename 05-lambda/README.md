# Deploy Lambda stack (in us-east-1)

Note that you'll need an S3 bucket to hold the deployed code.

```
$ aws cloudformation package \
  --region us-east-1 \
  --s3-bucket oscon-static-lambda-code \
  --template-file lambda.yml \
  --output-template-file lambda-packaged.yml

$ aws cloudformation deploy \
  --region us-east-1 \
  --capabilities CAPABILITY_IAM \
  --template-file lambda-packaged.yml \
  --stack-name oscon-lambda
```



# Update the CloudFront stack
