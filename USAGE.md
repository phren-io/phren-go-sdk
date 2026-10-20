<!-- Start SDK Example Usage [usage] -->
```go
package main

import (
	"context"
	phren "github.com/phren-io/phren-go-sdk"
	"log"
)

func main() {
	ctx := context.Background()

	s := phren.New()

	res, err := s.Organizations.List(ctx)
	if err != nil {
		log.Fatal(err)
	}
	if res.Organizations != nil {
		// handle response
	}
}

```
<!-- End SDK Example Usage [usage] -->