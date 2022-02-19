# cfn-variable-repository
 - cloudformation templates do not support variables and parameters in a template cannot reference other parameters
 - cfn-variable-repository is a cloudformation custom-resource to define and refer to dynamic variables within the cloudformation stack lifecycle


 - define your variables in the `CfnVariableRepository.Repository`, call them `CfnVariableRepository.<VariableName>` as many times as you need
 - see implementation [example](template-implementation.yaml)
 - do not use for secrets or sensitive data

## deployment
- deploy cfn-variable-repository 
```shell
aws cloudformation deploy --template-file ./template.yaml --stack-name variable-repository --capabilities CAPABILITY_NAMED_IAM
```

- implement and use a cfn-variable-repository
```shell
aws cloudformation deploy --template-file ./template-implementation.yaml --stack-name variable-repository-implementation --capabilities CAPABILITY_NAMED_IAM
```

- debug
```
aws logs tail "/aws/lambda/cfn-variable-repository" --follow
```

```shell
aws cloudformation describe-stacks --stack-name variable-repository-implementation
```
```shell
aws cloudformation describe-stacks --stack-name variable-repository-implementation --query 'Stacks[*].Outputs[*]'
```

- delete a stack
```shell
aws cloudformation delete-stack --stack-name variable-repository-implementation
```
