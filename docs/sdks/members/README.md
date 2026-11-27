# Members

## Overview

### Available Operations

* [List](#list) - List
* [Get](#get) - Get
* [MembersUpdate](#membersupdate) - Change a member's roles: admins make another member an admin, or make an
admin a plain member. Demoting the organization's last admin fails with
409.
* [Delete](#delete) - Remove a member. Admins remove anyone, and members remove themselves to
leave. Removing the organization's last admin fails with 409.

## List

List

### Example Usage

<!-- UsageSnippet language="go" operationID="Members_list" method="get" path="/v1/organizations/{organization}/members" -->
```go
package main

import(
	"context"
	"os"
	phren "github.com/phren-io/phren-go-sdk"
	"github.com/phren-io/phren-go-sdk/models/operations"
	"log"
)

func main() {
    ctx := context.Background()

    s := phren.New(
        phren.WithSecurity(os.Getenv("PHREN_BEARER_AUTH")),
    )

    res, err := s.Members.List(ctx, operations.MembersListRequest{
        Organization: "acme",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ListMembersResponse != nil {
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

| Parameter                                                                      | Type                                                                           | Required                                                                       | Description                                                                    |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ |
| `ctx`                                                                          | [context.Context](https://pkg.go.dev/context#Context)                          | :heavy_check_mark:                                                             | The context to use for the request.                                            |
| `request`                                                                      | [operations.MembersListRequest](../../models/operations/memberslistrequest.md) | :heavy_check_mark:                                                             | The request object to use for the request.                                     |
| `opts`                                                                         | [][operations.Option](../../models/operations/option.md)                       | :heavy_minus_sign:                                                             | The options for this request.                                                  |

### Response

**[*operations.MembersListResponse](../../models/operations/memberslistresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403            | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Get

Get

### Example Usage

<!-- UsageSnippet language="go" operationID="Members_get" method="get" path="/v1/organizations/{organization}/members/{member}" -->
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

    res, err := s.Members.Get(ctx, "acme", "0196f1a2-7c3e-7d4a-9b1e-3f2a6c8d9e01", nil)
    if err != nil {
        log.Fatal(err)
    }
    if res.Member != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                                                       | Type                                                                                                                                                                                                                                                            | Required                                                                                                                                                                                                                                                        | Description                                                                                                                                                                                                                                                     | Example                                                                                                                                                                                                                                                         |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ctx`                                                                                                                                                                                                                                                           | [context.Context](https://pkg.go.dev/context#Context)                                                                                                                                                                                                           | :heavy_check_mark:                                                                                                                                                                                                                                              | The context to use for the request.                                                                                                                                                                                                                             |                                                                                                                                                                                                                                                                 |
| `organization`                                                                                                                                                                                                                                                  | `string`                                                                                                                                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                                                              | N/A                                                                                                                                                                                                                                                             | acme                                                                                                                                                                                                                                                            |
| `member`                                                                                                                                                                                                                                                        | `string`                                                                                                                                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                                                              | N/A                                                                                                                                                                                                                                                             | 0196f1a2-7c3e-7d4a-9b1e-3f2a6c8d9e01                                                                                                                                                                                                                            |
| `include`                                                                                                                                                                                                                                                       | [*components.Include](../../models/components/include.md)                                                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                                                              | Extra data to return. With `permissions`, each resource lists the methods<br/>the caller may call on it, and a list response the methods on the<br/>collection. Rules that depend on data, such as keeping the last admin, are<br/>still checked when the method is called. |                                                                                                                                                                                                                                                                 |
| `opts`                                                                                                                                                                                                                                                          | [][operations.Option](../../models/operations/option.md)                                                                                                                                                                                                        | :heavy_minus_sign:                                                                                                                                                                                                                                              | The options for this request.                                                                                                                                                                                                                                   |                                                                                                                                                                                                                                                                 |

### Response

**[*operations.MembersGetResponse](../../models/operations/membersgetresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## MembersUpdate

Change a member's roles: admins make another member an admin, or make an
admin a plain member. Demoting the organization's last admin fails with
409.

### Example Usage

<!-- UsageSnippet language="go" operationID="Members_update" method="patch" path="/v1/organizations/{organization}/members/{member}" -->
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

    res, err := s.Members.MembersUpdate(ctx, "acme", "0196f1b8-2d4f-7a1c-8e3b-5c6d7e8f9a02", components.MemberUpdate{
        Roles: []components.MemberRole{
            components.MemberRoleAdmin,
        },
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.Member != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                          | Type                                                               | Required                                                           | Description                                                        | Example                                                            |
| ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ |
| `ctx`                                                              | [context.Context](https://pkg.go.dev/context#Context)              | :heavy_check_mark:                                                 | The context to use for the request.                                |                                                                    |
| `organization`                                                     | `string`                                                           | :heavy_check_mark:                                                 | N/A                                                                | acme                                                               |
| `member`                                                           | `string`                                                           | :heavy_check_mark:                                                 | N/A                                                                | 0196f1b8-2d4f-7a1c-8e3b-5c6d7e8f9a02                               |
| `body`                                                             | [components.MemberUpdate](../../models/components/memberupdate.md) | :heavy_check_mark:                                                 | N/A                                                                |                                                                    |
| `opts`                                                             | [][operations.Option](../../models/operations/option.md)           | :heavy_minus_sign:                                                 | The options for this request.                                      |                                                                    |

### Response

**[*operations.MembersUpdateResponse](../../models/operations/membersupdateresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404, 409  | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Delete

Remove a member. Admins remove anyone, and members remove themselves to
leave. Removing the organization's last admin fails with 409.

### Example Usage

<!-- UsageSnippet language="go" operationID="Members_delete" method="delete" path="/v1/organizations/{organization}/members/{member}" -->
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

    res, err := s.Members.Delete(ctx, "<value>", "<value>")
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
| `member`                                                 | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.MembersDeleteResponse](../../models/operations/membersdeleteresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404, 409  | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |