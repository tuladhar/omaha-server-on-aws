AWS_ARGS=--profile $(AWS_PROFILE) --region $(AWS_REGION)

STACK:=rds
TEMPLATE:=rds.yaml
ENV_LABEL?=omaha
ENV_TYPE?=nonprod

STACK_NAME:=$(ENV_LABEL)-$(ENV_TYPE)-$(STACK)

DB_INSTANCE_TYPE:=db.t3.small
DB_INSTANCE_IDENTIFIER:=$(STACK_NAME)
MULTI_AZ:=true

DB_USERNAME=master
DB_PASSWORD=dGVzdAoAEWxd

STACK_PARAMS:=ParameterKey=EnvironmentName,ParameterValue=$(ENV_LABEL) ParameterKey=EnvironmentType,ParameterValue=$(ENV_TYPE) ParameterKey=DBInstanceType,ParameterValue=$(DB_INSTANCE_TYPE) ParameterKey=DBInstanceIdentifier,ParameterValue=$(DB_INSTANCE_IDENTIFIER) ParameterKey=MultiAZ,ParameterValue=$(MULTI_AZ) ParameterKey=DBUsername,ParameterValue=$(DB_USERNAME) ParameterKey=DBPassword,ParameterValue=$(DB_PASSWORD)

create-stack:
	aws cloudformation create-stack --stack-name $(STACK_NAME) --template-body file://`pwd`/$(TEMPLATE) $(AWS_ARGS) --parameters $(STACK_PARAMS)

create-change-set:
	aws cloudformation create-change-set --stack-name $(STACK_NAME) --change-set-name $(STACK_NAME)-$(shell date +%s) --template-body file://`pwd`/$(TEMPLATE) $(AWS_ARGS) --parameters $(STACK_PARAMS)

delete-stack:
	aws cloudformation delete-stack --stack-name $(STACK_NAME) $(AWS_ARGS)
