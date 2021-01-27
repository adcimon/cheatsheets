# Go

<p align="center"><img align="center" src="go.png"></p>

[Go](https://golang.org/) is an open source programming language that makes it easy to build simple, reliable, and efficient software.

## General

Print the version.
```
go version
```

Compile and run a program.
```
go run <name>
```

Compile packages and dependencies.
```
go build <name>
```

Compile and install packages and dependencies.
```
go install <name>
```

Print environment information.
```
go env
```

## Modules

Activate modules.
```
go env -w GO111MODULE=on
```

Create a new module, initializing the `go.mod` file.
```
go mod init
```

Add dependencies to the module and install them.
```
go get
```

Remove unused dependencies.
```
go mod tidy
```

Print the module dependencies.
```
go list -m all
```
