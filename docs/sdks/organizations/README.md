# Organizations

## Overview

### Available Operations

* [List](#list) - List the organizations the caller can access.
* [Create](#create) - Create an organization.
* [Get](#get) - Get an organization.
* [Delete](#delete) - Soft-delete an organization. It can be undeleted until `purges_at`.
* [Undelete](#undelete) - Restore a soft-deleted organization (AIP-164).

## List

List the organizations the caller can access.

### Example Usage

<!-- UsageSnippet language="go" operationID="Organizations_list" method="get" path="/organizations" -->
```go
package main

import(
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

### Parameters

| Parameter                                                   | Type                                                        | Required                                                    | Description                                                 |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| `ctx`                                                       | [context.Context](https://pkg.go.dev/context#Context)       | :heavy_check_mark:                                          | The context to use for the request.                         |
| `pageSize`                                                  | `*int`                                                      | :heavy_minus_sign:                                          | Maximum number of results to return.                        |
| `pageToken`                                                 | `*string`                                                   | :heavy_minus_sign:                                          | Token from a previous page's links, to fetch the next page. |
| `filter`                                                    | `*string`                                                   | :heavy_minus_sign:                                          | AIP-160 filter expression.                                  |
| `showDeleted`                                               | `*bool`                                                     | :heavy_minus_sign:                                          | Include soft-deleted resources in the results.              |
| `opts`                                                      | [][operations.Option](../../models/operations/option.md)    | :heavy_minus_sign:                                          | The options for this request.                               |

### Response

**[*operations.OrganizationsListResponse](../../models/operations/organizationslistresponse.md), error**

### Errors

| Error Type                | Status Code               | Content Type              |
| ------------------------- | ------------------------- | ------------------------- |
| apierrors.BadRequestError | 400                       | application/problem+json  |
| apierrors.ForbiddenError  | 403                       | application/problem+json  |
| apierrors.APIError        | 4XX, 5XX                  | \*/\*                     |

## Create

Create an organization.

### Example Usage

<!-- UsageSnippet language="go" operationID="Organizations_create" method="post" path="/organizations" -->
```go
package main

import(
	"context"
	phren "github.com/phren-io/phren-go-sdk"
	"github.com/phren-io/phren-go-sdk/models/components"
	"log"
)

func main() {
    ctx := context.Background()

    s := phren.New()

    res, err := s.Organizations.Create(ctx, "<id>", components.OrganizationInput{
        DisplayName: "Blanca_Hettinger",
        State: components.OrganizationStateRestoring,
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

| Parameter                                                                    | Type                                                                         | Required                                                                     | Description                                                                  |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `ctx`                                                                        | [context.Context](https://pkg.go.dev/context#Context)                        | :heavy_check_mark:                                                           | The context to use for the request.                                          |
| `organizationID`                                                             | `string`                                                                     | :heavy_check_mark:                                                           | ID of the new organization; becomes the last segment of its name.            |
| `body`                                                                       | [components.OrganizationInput](../../models/components/organizationinput.md) | :heavy_check_mark:                                                           | N/A                                                                          |
| `opts`                                                                       | [][operations.Option](../../models/operations/option.md)                     | :heavy_minus_sign:                                                           | The options for this request.                                                |

### Response

**[*operations.OrganizationsCreateResponse](../../models/operations/organizationscreateresponse.md), error**

### Errors

| Error Type                | Status Code               | Content Type              |
| ------------------------- | ------------------------- | ------------------------- |
| apierrors.BadRequestError | 400                       | application/problem+json  |
| apierrors.ForbiddenError  | 403                       | application/problem+json  |
| apierrors.ConflictError   | 409                       | application/problem+json  |
| apierrors.APIError        | 4XX, 5XX                  | \*/\*                     |

## Get

Get an organization.

### Example Usage

<!-- UsageSnippet language="go" operationID="Organizations_get" method="get" path="/organizations/{organization}" -->
```go
package main

import(
	"context"
	phren "github.com/phren-io/phren-go-sdk"
	"log"
)

func main() {
    ctx := context.Background()

    s := phren.New()

    res, err := s.Organizations.Get(ctx, "<value>")
    if err != nil {
        log.Fatal(err)
    }
    if res.Organization != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `organization`                                           | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.OrganizationsGetResponse](../../models/operations/organizationsgetresponse.md), error**

### Errors

| Error Type                | Status Code               | Content Type              |
| ------------------------- | ------------------------- | ------------------------- |
| apierrors.BadRequestError | 400                       | application/problem+json  |
| apierrors.ForbiddenError  | 403                       | application/problem+json  |
| apierrors.NotFoundError   | 404                       | application/problem+json  |
| apierrors.APIError        | 4XX, 5XX                  | \*/\*                     |

## Delete

Soft-delete an organization. It can be undeleted until `purges_at`.

### Example Usage

<!-- UsageSnippet language="go" operationID="Organizations_delete" method="delete" path="/organizations/{organization}" -->
```go
package main

import(
	"context"
	phren "github.com/phren-io/phren-go-sdk"
	"log"
)

func main() {
    ctx := context.Background()

    s := phren.New()

    res, err := s.Organizations.Delete(ctx, "<value>", nil)
    if err != nil {
        log.Fatal(err)
    }
    if res.Organization != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `organization`                                           | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `force`                                                  | `*bool`                                                  | :heavy_minus_sign:                                       | Also delete the organization's child resources.          |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.OrganizationsDeleteResponse](../../models/operations/organizationsdeleteresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ForbiddenError | 403                      | application/problem+json |
| apierrors.NotFoundError  | 404                      | application/problem+json |
| apierrors.ConflictError  | 409                      | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Undelete

Restore a soft-deleted organization (AIP-164).

### Example Usage

<!-- UsageSnippet language="go" operationID="Organizations_undelete" method="post" path="/organizations/{organization}:undelete" -->
```go
package main

import(
	"context"
	phren "github.com/phren-io/phren-go-sdk"
	"log"
)

func main() {
    ctx := context.Background()

    s := phren.New()

    res, err := s.Organizations.Undelete(ctx, "<value>")
    if err != nil {
        log.Fatal(err)
    }
    if res.Organization != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `organization`                                           | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.OrganizationsUndeleteResponse](../../models/operations/organizationsundeleteresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ForbiddenError | 403                      | application/problem+json |
| apierrors.NotFoundError  | 404                      | application/problem+json |
| apierrors.ConflictError  | 409                      | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |