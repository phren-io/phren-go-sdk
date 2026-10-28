<!-- Start SDK Example Usage [usage] -->
```go
package main

import (
	"context"
	phren "github.com/phren-io/phren-go-sdk"
	"log"
	"os"
)

func main() {
	ctx := context.Background()

	s := phren.New(
		phren.WithSecurity(os.Getenv("PHREN_BEARER_AUTH")),
	)

	res, err := s.Organizations.List(ctx, phren.Pointer[int](50), phren.Pointer("CiAKGjBpNDd2Nmp2"), phren.Pointer("state = \"ACTIVE\""), phren.Pointer(false))
	if err != nil {
		log.Fatal(err)
	}
	if res.ListOrganizationsResponse != nil {
		for {
			// handle items

			res, err = res.Next()

			if err != nil {
				// handle error
			}

			if res == nil {
				break
			}
		}
	}
}

```
<!-- End SDK Example Usage [usage] -->