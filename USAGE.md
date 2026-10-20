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

	res, err := s.Widgets.ListWidgets(ctx)
	if err != nil {
		log.Fatal(err)
	}
	if res.WidgetList != nil {
		// handle response
	}
}

```
<!-- End SDK Example Usage [usage] -->