# !! WARNING !!
This repository forked by "github.com/nerd2/gexto"

This repository extend fs struct. Add List() method.

Below sample.
``` main.go
package main

import (
	"fmt"
	"io/ioutil"
	"log"
	"os"
	"strings"


	// go mod replace  "github.com/nerd2/gexto" => "github.com/masahiro331/gexto"
	"github.com/nerd2/gexto"
)

func main() {
	if len(os.Args) < 2 {
		log.Fatal("required [ext4] argument")
	}

	fs, _ := gexto.NewFileSystem(os.Args[1])
	files, _ := fs.List()
	for _, filename := range files {
		targetFile := "ANY FILES"
		if len(os.Args) == 3 {
			targetFile = os.Args[2]
		}
		if strings.Contains(filename, targetFile) {
			g, _ := fs.Open(filename)
			b, _ := ioutil.ReadAll(g)
			fmt.Println(string(b))
		}
	}
}
```


# gexto
## EXT2/EXT3/EXT4 Filesystem library for Golang

#### Introduction

Gexto is a Go library to allow read / write access to EXT2/3/4 filesystems.

Created due to my eternal frustration at the crazy world of guestfish, where starting a VM containing a separate and complete linux kernel is apparently the only non-root way of editing a filesystem image.

Aims to provide an "os."-like interface to the filesystem with file objects behaving basically how you would expect them to.

#### Minimal Example

Error checking omitted for brevity

```
import (
  "log"
  "github.com/nerd2/gexto"
)

func main() {
  fs, _ := gexto.NewFileSystem("file.ext4")

  f, _ := fs.Create("/test")
  f.Write([]byte("hello world")
  f.Close()

  g, _ := fs.Open("/another/file")
  log.Println(ioutil.ReadAll(file))
}
```

#### Testing

Note that testing requires (passwordless) sudo, in order that the test filesystems can be mounted.




