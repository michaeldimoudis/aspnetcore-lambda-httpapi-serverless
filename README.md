### Source code for blog:
# ASP.NET Core Serverless Web API running in AWS Lambda, using API Gateway HTTP API, with a Lambda Warmer

Simply specifying `DomainName`, `CertificateArn`, and Route53 `HostedZoneId` in `aws-lambda-tools-defaults.json`, and then running `dotnet lambda deploy-serverless` will spin up the entire infrastructure (HTTP API for Amazon API Gateway) and an ASP.NET Core Web API (running inside a Lambda) in minutes, ready to serve requests in a serverless and scalable way.

Remember to also choose an existing `s3-bucket` for your assets in `aws-lambda-tools-defaults.json`.

Once deployed just hit the API endpoint https://api.mydomain.com/api/values to make sure it's all working. (change to use your own domain name)

If your DNS is hosted elsewhere (or in another AWS account), just remove the `DNSRecordA` resource in `serverless.template`, and update the CNAME manually.

If you don't want a domain name (might be the case for Hackathons), also remove the `ApiGatewayDomainName` and `ApiGatewayBasePathMapping` resources in `serverless.template`, and you can hit your API via the API Gateway generated URL, which will be outputted as `ApiURL`.

A Lambda Warmer is also included doing an effective job in forgoing cold starts by specifying the number of instances you want to keep warm.

A CodeBuild `buildspec.yaml` file is provided to deploy this out. I recommend choosing the `aws/codebuild/amazonlinux2-x86_64-standard:3.0` environment image, as `PublishReadyToRun` is set to `true` to further improve the performance of the API.

If deploying locally from a Windows PC, set `PublishReadyToRun` to `false` in the `.csproj` file. You must have the .NET Core 3.1 SDK installed, as well as the Amazon.Lambda.Tools `dotnet tool install -g Amazon.Lambda.Tools`.

Blog post at [https://medium.com/@michaeldimoudis/asp-net-core-serverless-web-api-running-in-aws-lambda-using-api-gateway-http-api-a-lambdawarmer-6d31cdd6d3f5](https://medium.com/@michaeldimoudis/asp-net-core-serverless-web-api-running-in-aws-lambda-using-api-gateway-http-api-a-lambdawarmer-6d31cdd6d3f5)

