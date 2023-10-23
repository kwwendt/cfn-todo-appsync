# Todo API

This folder provides the implementation for a Todo API implemented with AppSync JavaScript resolvers. It provides a sample `buildspec.yml` file which can be used inside CodeBuild to dynamically upload the schema and resolver files to Amazon S3 and reference them within the `template.yaml` file.
The API allows you to interact with a Todo type:

```graphql
type Todo {
  id: ID!
  title: String
  description: String
  owner: String
}
```

The [resolvers](./resolvers/) folder contains the code for the resolvers. When you keep resolver code separate, you can run automation tests on the resolver code to verify it's functional before updating your CloudFormation template to use the new code. In addition, keeping the code files separate allows you to version each file individually in your source code repository of choice.

## CI/CD pipeline for this repo

First, you can create an AWS CodeCommit repository or another source location for this code. Next, you should create an AWS CodePipeline with the following stages:
- Source stage - CodeCommit or another source repository
- Build stage - CodeBuild. This is where you can reference the `buildspec_dev.yml` file in this repository.
- Deploy stage - CodeDeploy (deploying to CloudFormation)