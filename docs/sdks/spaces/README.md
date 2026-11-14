# Spaces

## Overview

### Available Operations

* [List](#list) - List the spaces in the organization the caller can see.
* [Create](#create) - Create. The project's admins create spaces in it.
* [Get](#get) - Get

## List

List the spaces in the organization the caller can see.

### Example Usage

<!-- UsageSnippet language="go" operationID="Spaces_list" method="get" path="/v1/organizations/{organization}/spaces" -->
```go
package main

import(
	"context"
	"os"
	phren "github.com/phren-io/phren-go-sdk"
	"log"
)

func main() {
    ctx := context.Background()

    s := phren.New(
        phren.WithSecurity(os.Getenv("PHREN_BEARER_AUTH")),
    )

    res, err := s.Spaces.List(ctx, "acme", phren.Pointer[int](50), nil, nil)
    if err != nil {
        log.Fatal(err)
    }
    if res.ListSpacesResponse != nil {
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

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              | Example                                                  |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |                                                          |
| `organization`                                           | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      | acme                                                     |
| `pageSize`                                               | `*int`                                                   | :heavy_minus_sign:                                       | Maximum number of results to return.                     | 50                                                       |
| `pageToken`                                              | `*string`                                                | :heavy_minus_sign:                                       | Token from a previous response's nextPageToken.          |                                                          |
| `filter`                                                 | `*string`                                                | :heavy_minus_sign:                                       | AIP-160 filter expression.                               |                                                          |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.SpacesListResponse](../../models/operations/spaceslistresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403            | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Create

Create. The project's admins create spaces in it.

### Example Usage

<!-- UsageSnippet language="go" operationID="Spaces_create" method="post" path="/v1/organizations/{organization}/spaces" -->
```go
package main

import(
	"context"
	"os"
	phren "github.com/phren-io/phren-go-sdk"
	"github.com/phren-io/phren-go-sdk/models/components"
	"log"
)

func main() {
    ctx := context.Background()

    s := phren.New(
        phren.WithSecurity(os.Getenv("PHREN_BEARER_AUTH")),
    )

    res, err := s.Spaces.Create(ctx, "acme", "notes", components.CreateSpace{
        Project: "organizations/acme/teams/core/projects/agent",
        DisplayName: "Notes",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.Space != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                             | Type                                                                                  | Required                                                                              | Description                                                                           | Example                                                                               |
| ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| `ctx`                                                                                 | [context.Context](https://pkg.go.dev/context#Context)                                 | :heavy_check_mark:                                                                    | The context to use for the request.                                                   |                                                                                       |
| `organization`                                                                        | `string`                                                                              | :heavy_check_mark:                                                                    | N/A                                                                                   | acme                                                                                  |
| `spaceID`                                                                             | `string`                                                                              | :heavy_check_mark:                                                                    | N/A                                                                                   | notes                                                                                 |
| `body`                                                                                | [components.CreateSpace](../../models/components/createspace.md)                      | :heavy_check_mark:                                                                    | N/A                                                                                   | {<br/>"project": "organizations/acme/teams/core/projects/agent",<br/>"displayName": "Notes"<br/>} |
| `opts`                                                                                | [][operations.Option](../../models/operations/option.md)                              | :heavy_minus_sign:                                                                    | The options for this request.                                                         |                                                                                       |

### Response

**[*operations.SpacesCreateResponse](../../models/operations/spacescreateresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 409       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Get

Get

### Example Usage

<!-- UsageSnippet language="go" operationID="Spaces_get" method="get" path="/v1/organizations/{organization}/spaces/{space}" -->
```go
package main

import(
	"context"
	"os"
	phren "github.com/phren-io/phren-go-sdk"
	"log"
)

func main() {
    ctx := context.Background()

    s := phren.New(
        phren.WithSecurity(os.Getenv("PHREN_BEARER_AUTH")),
    )

    res, err := s.Spaces.Get(ctx, "acme", "notes")
    if err != nil {
        log.Fatal(err)
    }
    if res.Space != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              | Example                                                  |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |                                                          |
| `organization`                                           | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      | acme                                                     |
| `space`                                                  | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      | notes                                                    |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.SpacesGetResponse](../../models/operations/spacesgetresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |