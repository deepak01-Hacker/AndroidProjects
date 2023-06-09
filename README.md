# FE RECOMMENDATION

Provides the recommended FE for a particular job given appropriate inputs. This has been implemented using a huggingface SentenceTransformer model(all-MiniLM-L6-v2). The recommended fe's are selected from two harcoded csv's.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [Features](#features)
- [Contributing](#contributing)

## Installation

### 1. Install and configure the AWS CLI:
```bash
$ aws configure
$ aws ecr get-login-password --region <AWS_REGION> | docker login --username AWS --password-stdin <AWS_ACCOUNT_ID>.dkr.ecr.<AWS_REGION>.amazonaws.com
```

### 2. Build your Docker image:

Fe Recommendation consists of below two seprate components <br>
**controller**<br>
**sqs_event_handler**<br>

Go to each of the above directory and execute the below commands
```bash
$ docker build -t <REPOSITORY_NAME> .
$ docker tag <REPOSITORY_NAME>:latest <AWS_ACCOUNT_ID>.dkr.ecr.<AWS_REGION>.amazonaws.com/<REPOSITORY_NAME>:latest
$ docker push <AWS_ACCOUNT_ID>.dkr.ecr.<AWS_REGION>.amazonaws.com/<REPOSITORY_NAME>:latest
```

## Usage

There is event bridge running on aws and any job created with in the 5 min it will trigger fe recommendation.<br>
To manually run the fe recommendation use the below endpoint.
```bash
https://www.flocareer.com/dynamic/support/triggerFeRecommendation/?req_id=36&title=MachineLearning&min_experience=2&required_skill=python<
```

## Features

This program takes the parameter from 'triggerFeRecommendation/' this endpoint and pushes into aws queue. Which inturm triggers lambda function to execute the Fe Recommendation.

## Contributing

**DEV TEAM** 
