# Update the CloudFormation stack

```
aws cloudformation update-stack \
  --template-body cfn.yml \
  --stack-name oscon-static \
  --parameters ParameterKey=DomainName,ParameterValue=2018.oscon.symphonia.io \
               ParameterKey=HostedZoneName,ParameterValue=oscon.symphonia.io.
```

# Open the site using the domain name

```
open "http://2018.oscon.symphonia.io"
```
