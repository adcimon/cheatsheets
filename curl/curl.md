# cURL

<p align="center"><img align="center" src="curl.png"></p>

[cURL](https://curl.se/) is a command line tool and library for transferring data with URL syntax.

## Table of Contents

* [Basic](#Basic)
* [HTTP](#http)

## Basic

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
```

Put.
```
curl --request PUT <url>
```

Delete.
```
curl --request DELETE <url>
```
