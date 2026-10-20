# Organizations

## Overview

### Available Operations

* [List](#list)
* [Create](#create)
* [Get](#get)
* [Delete](#delete)

## List

### Example Usage

<!-- UsageSnippet language="go" operationID="Organizations_listOrganizations" method="get" path="/organizations" -->
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

    res, err := s.Organizations.List(ctx)
    if err != nil {
        log.Fatal(err)
    }
    if res.Organizations != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.OrganizationsListOrganizationsResponse](../../models/operations/organizationslistorganizationsresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## Create

### Example Usage

<!-- UsageSnippet language="go" operationID="Organizations_createOrganization" method="post" path="/organizations" -->
```go
package main

import(
	"context"
	phren "github.com/phren-io/phren-go-sdk"
	"github.com/phren-io/phren-go-sdk/models/components"
	"github.com/phren-io/phren-go-sdk/types"
	"log"
)

func main() {
    ctx := context.Background()

    s := phren.New()

    res, err := s.Organizations.Create(ctx, components.Organization{
        UID: "<id>",
        ID: "<id>",
        Owner: "<value>",
        DisplayName: "Carrie29",
        State: components.OrganizationStatePurging,
        CreateTime: types.MustTimeFromString("2025-01-20T10:40:06.722Z"),
        UpdateTime: types.MustTimeFromString("2025-11-20T15:31:52.952Z"),
        PurgeTime: types.MustTimeFromString("2025-04-14T23:45:49.623Z"),
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

| Parameter                                                          | Type                                                               | Required                                                           | Description                                                        |
| ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ |
| `ctx`                                                              | [context.Context](https://pkg.go.dev/context#Context)              | :heavy_check_mark:                                                 | The context to use for the request.                                |
| `request`                                                          | [components.Organization](../../models/components/organization.md) | :heavy_check_mark:                                                 | The request object to use for the request.                         |
| `opts`                                                             | [][operations.Option](../../models/operations/option.md)           | :heavy_minus_sign:                                                 | The options for this request.                                      |

### Response

**[*operations.OrganizationsCreateOrganizationResponse](../../models/operations/organizationscreateorganizationresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## Get

### Example Usage

<!-- UsageSnippet language="go" operationID="Organizations_getOrganization" method="get" path="/organizations/{organizationId}" -->
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

    res, err := s.Organizations.Get(ctx, "<id>")
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
| `organizationID`                                         | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.OrganizationsGetOrganizationResponse](../../models/operations/organizationsgetorganizationresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |

## Delete

### Example Usage

<!-- UsageSnippet language="go" operationID="Organizations_deleteOrganization" method="delete" path="/organizations/{organizationId}" -->
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

    res, err := s.Organizations.Delete(ctx, "<id>")
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
| `organizationID`                                         | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.OrganizationsDeleteOrganizationResponse](../../models/operations/organizationsdeleteorganizationresponse.md), error**

### Errors

| Error Type         | Status Code        | Content Type       |
| ------------------ | ------------------ | ------------------ |
| apierrors.APIError | 4XX, 5XX           | \*/\*              |