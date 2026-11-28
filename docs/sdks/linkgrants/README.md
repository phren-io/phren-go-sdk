# LinkGrants

## Overview

### Available Operations

* [List](#list) - List who may link the space as a source. Its admins can.
* [Create](#create) - Grant a project, or the whole organization, linking. Its admins can.
* [Delete](#delete) - Revoke a grant. Every source it was allowing is removed in the same
call; sources still allowed another way (the same project, another
grant) stay.

## List

List who may link the space as a source. Its admins can.

### Example Usage

<!-- UsageSnippet language="go" operationID="LinkGrants_list" method="get" path="/v1/organizations/{organization}/spaces/{space}/linkGrants" -->
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

    res, err := s.LinkGrants.List(ctx, "<value>", "<value>", phren.Pointer[int](50), nil)
    if err != nil {
        log.Fatal(err)
    }
    if res.ListLinkGrantsResponse != nil {
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

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `organization`                                           | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `space`                                                  | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `pageSize`                                               | `*int`                                                   | :heavy_minus_sign:                                       | Maximum number of results to return.                     |
| `pageToken`                                              | `*string`                                                | :heavy_minus_sign:                                       | Token from a previous response's nextPageToken.          |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.LinkGrantsListResponse](../../models/operations/linkgrantslistresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Create

Grant a project, or the whole organization, linking. Its admins can.

### Example Usage

<!-- UsageSnippet language="go" operationID="LinkGrants_create" method="post" path="/v1/organizations/{organization}/spaces/{space}/linkGrants" -->
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

    res, err := s.LinkGrants.Create(ctx, "acme", "style-guide", components.CreateLinkGrant{
        Grantee: "organizations/acme/projects/agent",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.LinkGrant != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                | Type                                                                     | Required                                                                 | Description                                                              | Example                                                                  |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| `ctx`                                                                    | [context.Context](https://pkg.go.dev/context#Context)                    | :heavy_check_mark:                                                       | The context to use for the request.                                      |                                                                          |
| `organization`                                                           | `string`                                                                 | :heavy_check_mark:                                                       | N/A                                                                      | acme                                                                     |
| `space`                                                                  | `string`                                                                 | :heavy_check_mark:                                                       | N/A                                                                      | style-guide                                                              |
| `body`                                                                   | [components.CreateLinkGrant](../../models/components/createlinkgrant.md) | :heavy_check_mark:                                                       | N/A                                                                      | {<br/>"grantee": "organizations/acme/projects/agent"<br/>}               |
| `opts`                                                                   | [][operations.Option](../../models/operations/option.md)                 | :heavy_minus_sign:                                                       | The options for this request.                                            |                                                                          |

### Response

**[*operations.LinkGrantsCreateResponse](../../models/operations/linkgrantscreateresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 409       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Delete

Revoke a grant. Every source it was allowing is removed in the same
call; sources still allowed another way (the same project, another
grant) stay.

### Example Usage

<!-- UsageSnippet language="go" operationID="LinkGrants_delete" method="delete" path="/v1/organizations/{organization}/spaces/{space}/linkGrants/{grant}" -->
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

    res, err := s.LinkGrants.Delete(ctx, "<value>", "<value>", "<value>")
    if err != nil {
        log.Fatal(err)
    }
    if res != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `organization`                                           | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `space`                                                  | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `grant`                                                  | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.LinkGrantsDeleteResponse](../../models/operations/linkgrantsdeleteresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404, 409  | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |