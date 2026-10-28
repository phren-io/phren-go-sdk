# Organizations

## Overview

### Available Operations

* [List](#list) - List the organizations the caller can access.
* [Get](#get) - Get an organization.
* [Create](#create) - Create an organization. Repeating the same request is idempotent.
* [Delete](#delete) - Soft-delete an organization. It can be undeleted until `purgesAt`.
* [Undelete](#undelete) - Restore a soft-deleted organization (AIP-164).

## List

List the organizations the caller can access.

### Example Usage: Fetch the next page of active organizations

<!-- UsageSnippet language="go" operationID="Organizations_list" method="get" path="/v1/organizations" example="Fetch the next page of active organizations" -->
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
### Example Usage: List organizations

<!-- UsageSnippet language="go" operationID="Organizations_list" method="get" path="/v1/organizations" example="List organizations" -->
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

    res, err := s.Organizations.List(ctx, phren.Pointer[int](50), nil, nil, phren.Pointer(false))
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

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `pageSize`                                               | `*int`                                                   | :heavy_minus_sign:                                       | Maximum number of results to return.                     |
| `pageToken`                                              | `*string`                                                | :heavy_minus_sign:                                       | Token from a previous response's nextPageToken.          |
| `filter`                                                 | `*string`                                                | :heavy_minus_sign:                                       | AIP-160 filter expression.                               |
| `showDeleted`                                            | `*bool`                                                  | :heavy_minus_sign:                                       | Include soft-deleted resources in the results.           |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.OrganizationsListResponse](../../models/operations/organizationslistresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403            | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Get

Get an organization.

### Example Usage

<!-- UsageSnippet language="go" operationID="Organizations_get" method="get" path="/v1/organizations/{organization}" example="Get an organization" -->
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

    res, err := s.Organizations.Get(ctx, "acme")
    if err != nil {
        log.Fatal(err)
    }
    if res.Organization != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              | Example                                                  |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |                                                          |
| `organization`                                           | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      | acme                                                     |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.OrganizationsGetResponse](../../models/operations/organizationsgetresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Create

Create an organization. Repeating the same request is idempotent.

### Example Usage

<!-- UsageSnippet language="go" operationID="Organizations_create" method="put" path="/v1/organizations/{organization}" example="Create an organization" -->
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

    res, err := s.Organizations.Create(ctx, "acme", components.CreateOrganization{
        DisplayName: "Acme Corp",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.Organization != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                      | Type                                                                           | Required                                                                       | Description                                                                    | Example                                                                        |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ |
| `ctx`                                                                          | [context.Context](https://pkg.go.dev/context#Context)                          | :heavy_check_mark:                                                             | The context to use for the request.                                            |                                                                                |
| `organization`                                                                 | `string`                                                                       | :heavy_check_mark:                                                             | ID of the new organization; becomes the last segment of its name.              | acme                                                                           |
| `body`                                                                         | [components.CreateOrganization](../../models/components/createorganization.md) | :heavy_check_mark:                                                             | N/A                                                                            | {<br/>"displayName": "Acme Corp"<br/>}                                         |
| `opts`                                                                         | [][operations.Option](../../models/operations/option.md)                       | :heavy_minus_sign:                                                             | The options for this request.                                                  |                                                                                |

### Response

**[*operations.OrganizationsCreateResponse](../../models/operations/organizationscreateresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 409       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Delete

Soft-delete an organization. It can be undeleted until `purgesAt`.

### Example Usage

<!-- UsageSnippet language="go" operationID="Organizations_delete" method="delete" path="/v1/organizations/{organization}" example="Delete an organization" -->
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

    res, err := s.Organizations.Delete(ctx, "acme", phren.Pointer(false))
    if err != nil {
        log.Fatal(err)
    }
    if res.Organization != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              | Example                                                  |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |                                                          |
| `organization`                                           | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      | acme                                                     |
| `force`                                                  | `*bool`                                                  | :heavy_minus_sign:                                       | Also delete the organization's child resources.          |                                                          |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.OrganizationsDeleteResponse](../../models/operations/organizationsdeleteresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 401, 403, 404, 409       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Undelete

Restore a soft-deleted organization (AIP-164).

### Example Usage

<!-- UsageSnippet language="go" operationID="Organizations_undelete" method="post" path="/v1/organizations/{organization}:undelete" example="Undelete an organization" -->
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

    res, err := s.Organizations.Undelete(ctx, "acme")
    if err != nil {
        log.Fatal(err)
    }
    if res.Organization != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              | Example                                                  |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |                                                          |
| `organization`                                           | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      | acme                                                     |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.OrganizationsUndeleteResponse](../../models/operations/organizationsundeleteresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 401, 403, 404, 409       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |