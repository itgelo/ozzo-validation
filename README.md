## Description

This is a fork of [ozzo-validation](https://github.com/go-ozzo/ozzo-validation) to return _all validation_ errors found in every field instead just one error per field and also _force validation_ even with empty data. For instructions on how to use refer to the original [README](https://github.com/go-ozzo/ozzo-validation/blob/master/README.md)

### Installation

Run the following command to install the package:

```
go get github.com/itgelo/ozzo-validation/v4
go get github.com/itgelo/ozzo-validation/v4/is
```

### Validating a Simple Value

For a simple value, such as a string or an integer, you may use `validation.Validate()` to validate it. For example,

```go
package main

import (
	"fmt"

	"github.com/itgelo/ozzo-validation/v4"
	"github.com/itgelo/ozzo-validation/v4/is"
)

func main() {
	data := "example"
	err := validation.Validate(data,
		validation.Required,        // not empty
		validation.Length(10, 100), // length between 10 and 100
		is.URL,                     // is a valid URL
	)
	fmt.Println(err)
	// Output:
	// the length must be between 10 and 100,must be a valid URL
}
```

Normally validation `Length`, `URL` etc it does not validate if the data is empty. If you still need to validate it you may use `.ForceValidateEmpty()` to _force_ validate it. For example,

```go
data := ""
err := validation.Validate(data,
	validation.Required,
	validation.Length(10, 100).ForceValidateEmpty(), // force validate
	is.URL.ForceValidateEmpty(),                     // force validate
)
fmt.Println(err)
// Output:
// cannot be blank,the length must be between 10 and 100,must be a valid URL
```
