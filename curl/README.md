# cURL

<p align="center"><img align="center" src="assets/curl.svg"></p>

[cURL](https://curl.se/) is a command line tool and library for transferring data with URL syntax.

## Index

* [General](#general)
* [HTTP](#http)

## General

Check version.
```
curl --version
```

Save the result to a file.
```
curl <url> -o <file>
curl <url> -O
```

## HTTP

Get.
```
curl --request GET <url>
```

Get only header.
```
curl --request GET --head <url>
```

Post.
```
curl --request POST <url>
curl --request POST --header "Content-Type: application/json" --data @<file> <url>
curl --request POST --header "Content-Type: application/json" --data '{"key": "value"}' <url>
curl --request POST --header "Content-Type: application/json" --data "{\"key\": \"value\"}" <url>
```

Put.
```
curl --request PUT <url>
```

Delete.
```
curl --request DELETE <url>
```
