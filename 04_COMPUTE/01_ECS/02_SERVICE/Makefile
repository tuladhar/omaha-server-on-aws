AWS_ARGS=--profile $(AWS_PROFILE) --region $(AWS_REGION)

STACK:=ecs-service
TEMPLATE:=service.yaml
ENV_LABEL?=omaha
ENV_TYPE?=nonprod

STACK_NAME:=$(ENV_LABEL)-$(ENV_TYPE)-$(STACK)

DB_USERNAME=master
DB_PASSWORD=dGVzdAoAEWxd
SECRET_KEY=dGVzdAoAEWxd

STACK_PARAMS:=ParameterKey=EnvironmentName,ParameterValue=$(ENV_LABEL) ParameterKey=EnvironmentType,ParameterValue=$(ENV_TYPE) ParameterKey=DBUsername,ParameterValue=$(DB_USERNAME) ParameterKey=DBPassword,ParameterValue=$(DB_PASSWORD) ParameterKey=SecretKey,ParameterValue=$(SECRET_KEY)

create-stack:
	aws cloudformation create-stack --stack-name $(STACK_NAME) --template-body file://`pwd`/$(TEMPLATE) $(AWS_ARGS) --parameters $(STACK_PARAMS)

create-change-set:
	aws cloudformation create-change-set --stack-name $(STACK_NAME) --change-set-name $(STACK_NAME)-$(shell date +%s) --template-body file://`pwd`/$(TEMPLATE) --capabilities CAPABILITY_IAM $(AWS_ARGS) --parameters $(USE_PREV_STACK_PARAMS)

delete-stack:
	aws cloudformation delete-stack --stack-name $(STACK_NAME) $(AWS_ARGS)
