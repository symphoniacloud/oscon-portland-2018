# Update the CloudFormation stack

```
aws cloudformation update-stack \
  --template-body file://cfn.yml \
  --stack-name oscon-static \
  --parameters ParameterKey=DomainName,ParameterValue=2018.oscon.symphonia.io \
               ParameterKey=HostedZoneName,ParameterValue=oscon.symphonia.io. \
               ParameterKey=ValidationDomain,ParameterValue=symphonia.io
```

# Validate the certificate (via email, or DNS)

# Open the site using the HTTPS protocol

```
open "https://2018.oscon.symphonia.io"
```
