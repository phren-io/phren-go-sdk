<!-- Start SDK Example Usage [usage] -->
```go
package main

import (
	"context"
	phren "github.com/phren-io/phren-go-sdk"
	"github.com/phren-io/phren-go-sdk/models/operations"
	"log"
	"os"
)

func main() {
	ctx := context.Background()

	s := phren.New(
		phren.WithSecurity(os.Getenv("PHREN_BEARER_AUTH")),
	)

	res, err := s.Organizations.List(ctx, operations.OrganizationsListRequest{
		PageToken:   phren.Pointer("CiAKGjBpNDd2Nmp2"),
		Filter:      phren.Pointer("state != \"ACTIVE\""),
		ShowDeleted: phren.Pointer(true),
	})
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