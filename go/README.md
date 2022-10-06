# Go

<p align="center"><img align="center" width="50%" height="50%" src="assets/go.svg"></p>

[Go](https://golang.org/) is an open source programming language that makes it easy to build simple, reliable, and efficient software.

## Index

* [General](#general)
* [Modules](#modules)
* [CGO](#cgo)
* [More](#more)

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
env GOOS=<operating_system> GOARCH=<architecture> go build
```

Compile with the linker using static links.
```
go build -ldflags="-extldflags=-static"
```

Compile with the windows console hidden.
```
go build -ldflags="-Hwindowsgui"
```

Compile and install packages and dependencies.
```
go install
```

List available platforms.
```
go tool dist list
```

Use the built-in [data race detector](https://golang.org/doc/articles/race_detector).
```
go run -race main.go
go build -race
go build -race -o <name>
go install -race
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

Add a dependency to the module.
```
go get
```

Update all modules and their dependencies.
```
go get -u ./...
```

Update a module to the latest commit or to a branch.
```
go get -v -u github.com/user/repo@master
go get -v -u github.com/user/repo@develop
```

Remove unused dependencies.
```
go mod tidy
```

List the module dependencies.
```
go list -m all
go list -u -m all
```

Import local module (modify the `go.mod` file to find the module in the local file system).
```
replace github.com/adcimon/mymodule => ../mymodule
```

## CGO

[CGO](https://golang.org/pkg/cmd/cgo/) enables the creation of Go packages that call C code.

### Windows

In order to use CGO on Windows a gcc compiler is needed.
1. Download a [MinGW-W64](https://www.mingw-w64.org/) installer from [MinGW-W64 files](https://sourceforge.net/projects/mingw-w64/files/).
2. Install MinGW-W64 with `Architecture` to `x86_64` and `Threads` to `win32`.
3. Add `mingw64/bin` to the PATH environment variable.

### Call C code

The Go function `Print` calls the C function `fputs` (from the `stdio` library).
```
package main

/*
#include <stdio.h>
#include <stdlib.h>
*/
import "C"

import (
  "unsafe"
)

func Print (str string) () {
  cstr := C.CString(str)
  C.fputs(cstr, (*C.FILE)(C.stdout))
  C.free(unsafe.Pointer(cstr))
}

func main () () {
  Print("Hello World!")
}
```

### Use a DLL

Include the header (.h) and link the import library (.lib).
```
/*
#cgo CFLAGS: -I${SRCDIR}/include
#cgo LDFLAGS: -L${SRCDIR}/lib -lmylib
#include "MyLib.h"
*/
import "C"
```
Any occurrence of the string `${SRCDIR}` will be replaced by the absolute path to the directory containing the source file.

Copy the dynamic library (.dll) to the executable (.exe) directory.
```
MyProgram
├── main.exe
└── mylib.dll
```

### Create a DLL

Use `//export` directives to make Go functions accessible to C code. The `main` function is needed to make CGO compile the package as a C shared library.
```
package main

import "C"

import (
  "fmt"
)

//export hello
func hello () () {
  fmt.Printf("Hello World!")
}

func main () () {
}
```

Build the library.
```
go build -buildmode=c-shared -o hello.dll
```

Export the header file.
```
go tool cgo main.go
```

It generates C header and source files into the `_obj` directory.

## More

### Set string variable at build time

The [Go linker](https://pkg.go.dev/cmd/link) has an option to set the value of an uninitialised string variable:
```
-X importpath.name=value
  Set the value of the string variable in importpath named name to
```

For example:
```
package main

import "log"

var version string

func main() {
    log.Println(version)
}
```

Setting the `ldflags`:
```
go run -ldflags "-X main.version=1.0.0" main.go
```

### Embed icon and metadata into exe

1. Install MinGW.

2. Create the `main.exe.manifest` file.
```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">
<assemblyIdentity
    version="1.0.0.0"
    processorArchitecture="x86"
    name="controls"
    type="win32"
/>
<dependency>
    <dependentAssembly>
        <assemblyIdentity
            type="win32"
            name="Microsoft.Windows.Common-Controls"
            version="6.0.0.0"
            processorArchitecture="*"
            publicKeyToken="6595b64144ccf1df"
            language="*"
        />
    </dependentAssembly>
</dependency>
</assembly>
```
<br>

3. Create the `main.rc` file.
```
100 ICON    "main.ico"
100 24      "main.exe.manifest"
101 RCDATA  "content.zip"
```
<br>

4. Build.
```
windres -o main-res.syso main.rc && go build -i
```
