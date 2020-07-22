AWS_ARGS=--profile $(AWS_PROFILE) --region $(AWS_REGION)

STACK:=bucket
TEMPLATE:=bucket.yaml
ENV_LABEL?=omaha
ENV_TYPE?=nonprod

STACK_NAME:=$(ENV_LABEL)-$(ENV_TYPE)-$(STACK)

STACK_PARAMS:=ParameterKey=EnvironmentName,ParameterValue=$(ENV_LABEL) ParameterKey=EnvironmentType,ParameterValue=$(ENV_TYPE)
USE_PREV_STACK_PARAMS:=ParameterKey=EnvironmentName,ParameterValue=$(ENV_LABEL) ParameterKey=EnvironmentType,ParameterValue=$(ENV_TYPE)

create-stack:
	aws cloudformation create-stack --stack-name $(STACK_NAME) --template-body file://`pwd`/$(TEMPLATE) --capabilities CAPABILITY_IAM $(AWS_ARGS) --parameters $(STACK_PARAMS)

create-change-set:
	aws cloudformation create-change-set --stack-name $(STACK_NAME) --change-set-name $(STACK_NAME)-$(shell date +%s) --template-body file://`pwd`/$(TEMPLATE) --capabilities CAPABILITY_IAM $(AWS_ARGS) --parameters $(USE_PREV_STACK_PARAMS)

delete-stack:
	aws cloudformation delete-stack --stack-name $(STACK_NAME) $(AWS_ARGS)
