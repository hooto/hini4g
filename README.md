## hini4g

hooto INI file read library for golang.

Example:

``` go
package main

import (
	"fmt"

	"github.com/hooto/hini4g/hini"
)

func main() {

	ini_str := `
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
[remote "origin"]
	url = https://github.com/hooto/hini4g.git
	fetch = +refs/heads/*:refs/remotes/origin/*
`

	options, err := hini.ParseString(ini_str)
	if err == nil {
		fmt.Println("remote/origin/url : ", options.Value("remote/origin/url").String())

		if _, ok := options.ValueOK("core/filemode"); ok {
			fmt.Println("core/filemode : exist")
		}

		if _, ok := options.ValueOK("remote/none/url"); !ok {
			fmt.Println("remote/none/url : not exist")
		}
	}

	options, err = hini.ParseFile("/path/to/file.ini")
	if err == nil {
		fmt.Println("remote/origin/url : ", options.Value("remote/origin/url").String())
	}
}
```


Output:

``` shell
remote/origin/url :  https://github.com/hooto/hini4g.git
core/filemode : exist
remote/none/url : not exist
```
