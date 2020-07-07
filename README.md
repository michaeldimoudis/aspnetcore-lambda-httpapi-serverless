### Source code for blog:
# ASP.NET Core Serverless Web API running in AWS Lambda, using API Gateway HTTP API, with a Lambda Warmer

Simply specifying `DomainName`, `CertificateArn`, and Route53 `HostedZoneId` in `aws-lambda-tools-defaults.json`, and then running `dotnet lambda deploy-serverless` will spin up the entire infrastructure (HTTP API for Amazon API Gateway / Lambda) and an ASP.NET Core Web API in minutes, ready to serve requests in a serverless and scalable way.

Lambda Warmer is also included doing an effective job in forgoing cold starts by specifying the number of instances you want to keep warm.

A CodeBuild `buildspec.yaml` file is provided to deploy this out. I recommend choosing the `aws/codebuild/amazonlinux2-x86_64-standard:3.0` environment image, as `PublishReadyToRun` is set to `true` to further improve the performance of the API.

Once deployed just hit the API endpoint https://api.mydomain.com/api/values to make sure it's all working. (remember to use your own domain name)

Blog post at [https://medium.com/@michaeldimoudis/asp-net-core-serverless-web-api-running-in-aws-lambda-using-api-gateway-http-api-a-lambdawarmer-6d31cdd6d3f5](https://medium.com/@michaeldimoudis/asp-net-core-serverless-web-api-running-in-aws-lambda-using-api-gateway-http-api-a-lambdawarmer-6d31cdd6d3f5)

