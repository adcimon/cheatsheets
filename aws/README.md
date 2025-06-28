# AWS

</br>
<p align="center"><img align="center" width="30%" height="30%" src="assets/aws.svg"></p>

[Amazon Web Services (AWS)](https://aws.amazon.com/) provides on-demand cloud computing platforms and APIs to individuals, companies, and governments, on a metered, pay-as-you-go basis.

## Index

* [General](#general)
* [CLI](#cli)
* [Cognito](#cognito)
* [DCV](#dcv)
* [DynamoDB](#dynamodb)
* [SES](#ses)
* [S3](#s3)

## General

* Documentation: https://docs.aws.amazon.com
* JavaScript SDK: https://docs.aws.amazon.com/sdk-for-javascript/

## CLI

Install.
* https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

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

## DCV

[Desktop Cloud Visualization (DCV)](https://docs.aws.amazon.com/dcv/) is a remote visualization technology that delivers remote desktop and application streaming from any cloud or data center to any device over varying network conditions.

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

Send email command input.
```
{
	"FromEmailAddress": "from@email.com",
	"Destination": {
		"ToAddresses": [ "to@email.com" ]
	}
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
	}
}
```
* [Send raw email](https://docs.aws.amazon.com/ses/latest/dg/send-email-raw.html)

## S3

[Simple Storage Service (S3)](https://docs.aws.amazon.com/s3/) is a scalable, high-speed, web-based cloud storage service.

List buckets.
```
aws s3 ls
```

Download bucket.
```
aws s3 sync <uri> <local_path>
aws s3 sync s3://<name> <local_path>
aws s3 sync s3://<path> <local_path>
```
