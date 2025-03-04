# Kotaemon on AWS App Runner

An open-source RAG-based tool for chatting with your documents: https://cinnamon.github.io/kotaemon/ now available on a public endpoint.


## 1-Click Deployment

[![launch-stack.png](launch-stack.png)](https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=koatemon-on-aws-app-runner&templateURL=https://public-assets-vincent-claes.s3.eu-west-1.amazonaws.com/kotaemon-on-aws-app-runner/cloudformation.yaml)

- User: admin
- Password: admin

__Important__: Once it's deployed go to Resources > Users
Create a new user with admin privileges with a strong password and remove the 'admin' user.

```bash
export STACK_NAME=<stack-name>
aws cloudformation create-stack \
  --stack-name "${STACK_NAME}" \
  --template-body file://cloudformation.yaml \
  --parameters ParameterKey=ServiceName,ParameterValue=${STACK_NAME} \
  --capabilities CAPABILITY_NAMED_IAM
```

## Docker

### Docker build

```bash
docker build --platform linux/amd64 --progress plain --no-cache -t kotaemon .
```

### Docker push

```bash
export AWS_PROFILE=nonprod
aws ecr get-login-password --region eu-west-1 | docker login --username AWS --password-stdin 077590795309.dkr.ecr.eu-west-1.amazonaws.com
docker tag kotaemon:latest 077590795309.dkr.ecr.eu-west-1.amazonaws.com/kotaemon:latest
docker push 077590795309.dkr.ecr.eu-west-1.amazonaws.com/kotaemon:latest
```
