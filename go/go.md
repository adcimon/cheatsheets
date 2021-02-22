# Go

<p align="center"><img align="center" src="go.png"></p>

[Go](https://golang.org/) is an open source programming language that makes it easy to build simple, reliable, and efficient software.

## General

Print the version.
```
go version
```

Print environment information.
```
go env
```

Compile and run a program.
```
go run main.go
```

Compile packages and dependencies.
```
go build
go build -o <name>
```

Compile and install packages and dependencies.
```
go install
```

List available platforms.
```
go tool dist list
```

## Modules

Activate modules.
```
go env -w GO111MODULE=on
```

Create a new module, initializing the `go.mod` file.
```
go mod init
go mod init <name>
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

Import local module (modify the `go.mod` file to find the module in the local file system).
```
replace github.com/adcimon/mymodule => ../mymodule
```
