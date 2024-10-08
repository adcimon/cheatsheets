# AWS

</br>
<p align="center"><img align="center" width="30%" height="30%" src="assets/aws.svg"></p>

[Amazon Web Services (AWS)](https://aws.amazon.com/) provides on-demand cloud computing platforms and APIs to individuals, companies, and governments, on a metered, pay-as-you-go basis.

## Index

* [Install](#install)
* [General](#general)
* [Cognito](#cognito)
* [DynamoDB](#dynamodb)
* [SES](#ses)
* [S3](#s3)

## Install

Install the `aws` command-line tool.
* https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

## General

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

## Cognito

List user pools.
```
aws cognito-idp list-user-pools --max-results 10
```

## DynamoDB

Scan table.
```
aws dynamodb scan --table-name "<table>"
```
* [Scanning tables in DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Scan.html)

Get item.
```
aws dynamodb get-item --table-name "<table>" --key '{\"<key>\": {\"S\": \"<value>\"}}'
```

Update item.
```
aws dynamodb update-item --table-name "<table>"
	--key '{\"<key>\": {\"S\": \"<value>\"}}'
	--update-expression "SET #Name = :value"
	--expression-attribute-names '{\"#Name\": \"<attribute_name>\"}'
	--expression-attribute-values '{\":value\": {\"<attribute_type>\": \"<args.attribute_value>\"}}'
```

Delete item.
```
aws dynamodb delete-item --table-name "<table>" --key '{\"<key>\": {\"S\": \"<value>\"}}'
```

## SES

Send email command.
```
{
	"Content": {
		"Simple": {
			"Subject": {
				"Charset": "utf-8",
				"Data": "The subject"
			},
			"Body": {
				"Text": {
					"Charset": "utf-8",
					"Data": "The body"
				}
			}
		}
	},
	"FromEmailAddress": "from@email.com",
	"Destination": {
		"ToAddresses": [ "to@email.com" ]
	}
}
```

## S3

List buckets.
```
aws s3 ls
```
