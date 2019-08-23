﻿# go-fileversion


Package `fileversion` provides wrapper for windows version-information resource.

Package extracts this information from file:

![](https://github.com/bi-zone/go-fileversion/blob/version_info_fillinf/explorer_properties.png)



## Examples

Print version info from input file
```golang
package main

import (
	"fmt"
	"log"
	"os"

	"github.com/bi-zone/go-fileversion"
	"github.com/davecgh/go-spew/spew"
)

func main() {
	if len(os.Args) < 2 {
		log.Fatal("Usage: ./file_info.exe <image-path>")
	}
	f, err := fileversion.New(os.Args[1])
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println("CompanyName:", f.CompanyName())
	fmt.Println("FileDescription:", f.FileDescription())
	fmt.Println("FileVersion:", f.FileVersion())
	fmt.Println("InternalName:", f.InternalName())
	fmt.Println("LegalCopyright:", f.LegalCopyright())
	fmt.Println("OriginalFilename:", f.OriginalFilename())
	fmt.Println("ProductName:", f.ProductName())
	fmt.Println("ProductVersion:", f.ProductVersion())
	fmt.Println("Comments:", f.Comments())
	fmt.Println("FileVeLegalTrademarksrsion:", f.FileVeLegalTrademarksrsion())
	fmt.Println("PrivateBuild:", f.PrivateBuild())
	fmt.Println("SpecialBuild:", f.SpecialBuild())

	spew.Dump(f.FixedFileInfo)
}
```

You can create version info object with own-defined locale

```golang
f, err := fileversion.New(os.Args[1], fileversion.EnglishUnicode)
	if err != nil {
		log.Fatal(err)
	}
```

You can combine a locale with another language and another charset. Read the [docs](https://docs.microsoft.com/en-us/windows/win32/menurc/versioninfo-resource).
```golang
f, err := fileversion.New(os.Args[1], "041904b0") // Russian + Unicode
	if err != nil {
		log.Fatal(err)
	}
```

## Notes
The idea of locales handling was copied from [.NET Framework 4.8](https://referencesource.microsoft.com/#System/services/monitoring/system/diagnosticts/FileVersionInfo.cs,036c54a4aa10d39f,references)
