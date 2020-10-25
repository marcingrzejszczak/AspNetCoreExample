# Purpose

Sample project written in .net

# Running contract tests

It's enough for you to run `./scripts/runAcceptanceTests.sh` to

- Build a docker image with Artifactory (normally you would have that running / you could also use Git instead)
- We run the app on port `5000` in the `ContractTests` mode
- We run the Spring Cloud Contract docker image that has the `contracts` folder mounted with contracts
- From the mounted folder tests are generated against the running application
- Once the tests have passed stubs are generated and uploaded to Artifactory

# Runing stubs

It's enough for you to run `./scripts/runStubs.sh` to

- get stubs from Artifactory and run them on specified port with Wiremock
- once the stub runner is running you can test your api against defined contract tests

To learn more about stub runner go to: 

https://cloud.spring.io/spring-cloud-contract/reference/html/docker-project.html#docker-stubrunner

# Running the app locally

## Pre-requisites

* Installed .NET SDK 5.0
	* https://dotnet.microsoft.com/download/dotnet/5.0

## Build Application

From command line execute `dotnet build`

## Run application

From command line execute `dotnet run`

# Docker

## Docker build
`docker build -f src/AspNetCoreExample/Dockerfile  -t cdc-aspnetcoreexample .`

## Docker run - Production environment

`docker run -d -p 5000:80  cdc-aspnetcoreexample`

## Docker run - ContractTests environment

`docker run -d -e "ASPNETCORE_ENVIRONMENT=ContractTests" -p 5000:80 cdc-aspnetcoreexample`

# Swagger

http://localhost:5000/swagger - swagger ui
http://localhost:5000/api-docs - redoc


# Pipelines

Section describes commands that will be used by Cloud Foundry pipelines.

<b>Warning:<b> Output from below commands start with extra spaces in each line. Please make `left trim` (you can do it by piping to `xargs`)

e.g.

## Application name

`dotnet msbuild /nologo /t:cfpappname | xargs`

## Application version

`dotnet msbuild /nologo /t:cfpversion | xargs`

## Application GroupId

`dotnet msbuild /nologo /t:cfpgroupid | xargs`

## Application ArtifactId

`dotnet msbuild /nologo /t:cfpartifactid | xargs`

## Run UnitTests

`dotnet msbuild /nologo /t:CFPUnitTests | xargs`

## Run End 2 end tests

`dotnet msbuild /nologo /t:CFPE2eTests | xargs`

## Run Smoke Tests

`dotnet msbuild /nologo /t:CFPSmokeTests | xargs`

## Publish

`dotnet msbuild /nologo /t:CFPPublish /p:Configuration=Release`