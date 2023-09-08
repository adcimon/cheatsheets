# AWS

</br>
<p align="center"><img align="center" width="30%" height="30%" src="assets/aws.svg"></p>

[Amazon Web Services (AWS)](https://aws.amazon.com/) provides on-demand cloud computing platforms and APIs to individuals, companies, and governments, on a metered, pay-as-you-go basis.

# CLI

## Install

Install the `aws` command-line tool.
* https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

## Usage

Check version.
```
aws --version
```

Configure.
```
aws configure
```

Login with SSO.
```
aws configure sso
aws sso login
```

List services.
```
aws list-services
```

List S3 buckets.
```
aws s3 ls
```

List Cognito user pools.
```
aws cognito-idp list-user-pools --max-results 10
```
