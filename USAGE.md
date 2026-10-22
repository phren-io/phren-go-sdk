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

	res, err := s.Organizations.List(ctx, nil, nil, nil, nil)
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