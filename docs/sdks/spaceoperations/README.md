# SpaceOperations

## Overview

### Available Operations

* [List](#list) - List, newest first.
* [Get](#get) - Get
* [Cancel](#cancel) - Cancel a delete in flight: the delete stops, its operation is done with a
`Cancelled` error, and a new undelete operation restores the space.
Returns that undelete operation. Fails with 409 if the operation has
already finished (undelete the space instead) or is not a delete. The
admins of the space's project can cancel.
* [Wait](#wait) - Wait for the operation to finish. Returns it when it is done or when
`timeout` passes, whichever is first; check `done` and call again if it
is still running.

## List

List, newest first.

### Example Usage

<!-- UsageSnippet language="go" operationID="SpaceOperations_list" method="get" path="/v1/organizations/{organization}/spaces/{space}/operations" example="Deleted and undeleted" -->
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

    res, err := s.SpaceOperations.List(ctx, operations.SpaceOperationsListRequest{
        Organization: "acme",
        Space: "notes",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ListSpaceOperationsResponse != nil {
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

| Parameter                                                                                      | Type                                                                                           | Required                                                                                       | Description                                                                                    |
| ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| `ctx`                                                                                          | [context.Context](https://pkg.go.dev/context#Context)                                          | :heavy_check_mark:                                                                             | The context to use for the request.                                                            |
| `request`                                                                                      | [operations.SpaceOperationsListRequest](../../models/operations/spaceoperationslistrequest.md) | :heavy_check_mark:                                                                             | The request object to use for the request.                                                     |
| `opts`                                                                                         | [][operations.Option](../../models/operations/option.md)                                       | :heavy_minus_sign:                                                                             | The options for this request.                                                                  |

### Response

**[*operations.SpaceOperationsListResponse](../../models/operations/spaceoperationslistresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403            | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Get

Get

### Example Usage

<!-- UsageSnippet language="go" operationID="SpaceOperations_get" method="get" path="/v1/organizations/{organization}/spaces/{space}/operations/{operation}" -->
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

    res, err := s.SpaceOperations.Get(ctx, "acme", "notes", "019a8f3e-4b2c-7d1e-9f3a-2c4b6d8e0f11")
    if err != nil {
        log.Fatal(err)
    }
    if res.SpaceOperation != nil {
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
| `operation`                                              | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      | 019a8f3e-4b2c-7d1e-9f3a-2c4b6d8e0f11                     |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.SpaceOperationsGetResponse](../../models/operations/spaceoperationsgetresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Cancel

Cancel a delete in flight: the delete stops, its operation is done with a
`Cancelled` error, and a new undelete operation restores the space.
Returns that undelete operation. Fails with 409 if the operation has
already finished (undelete the space instead) or is not a delete. The
admins of the space's project can cancel.

### Example Usage

<!-- UsageSnippet language="go" operationID="SpaceOperations_cancel" method="post" path="/v1/organizations/{organization}/spaces/{space}/operations/{operation}:cancel" -->
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

    res, err := s.SpaceOperations.Cancel(ctx, "acme", "notes", "019a8f3e-4b2c-7d1e-9f3a-2c4b6d8e0f11")
    if err != nil {
        log.Fatal(err)
    }
    if res.SpaceOperation != nil {
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
| `operation`                                              | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      | 019a8f3e-4b2c-7d1e-9f3a-2c4b6d8e0f11                     |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.SpaceOperationsCancelResponse](../../models/operations/spaceoperationscancelresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404, 409  | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Wait

Wait for the operation to finish. Returns it when it is done or when
`timeout` passes, whichever is first; check `done` and call again if it
is still running.

### Example Usage

<!-- UsageSnippet language="go" operationID="SpaceOperations_wait" method="post" path="/v1/organizations/{organization}/spaces/{space}/operations/{operation}:wait" -->
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

    res, err := s.SpaceOperations.Wait(ctx, "acme", "notes", "019a8f3e-4b2c-7d1e-9f3a-2c4b6d8e0f11", phren.Pointer("10s"))
    if err != nil {
        log.Fatal(err)
    }
    if res.SpaceOperation != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                | Type                                                                                                                                                                                                                     | Required                                                                                                                                                                                                                 | Description                                                                                                                                                                                                              | Example                                                                                                                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `ctx`                                                                                                                                                                                                                    | [context.Context](https://pkg.go.dev/context#Context)                                                                                                                                                                    | :heavy_check_mark:                                                                                                                                                                                                       | The context to use for the request.                                                                                                                                                                                      |                                                                                                                                                                                                                          |
| `organization`                                                                                                                                                                                                           | `string`                                                                                                                                                                                                                 | :heavy_check_mark:                                                                                                                                                                                                       | N/A                                                                                                                                                                                                                      | acme                                                                                                                                                                                                                     |
| `space`                                                                                                                                                                                                                  | `string`                                                                                                                                                                                                                 | :heavy_check_mark:                                                                                                                                                                                                       | N/A                                                                                                                                                                                                                      | notes                                                                                                                                                                                                                    |
| `operation`                                                                                                                                                                                                              | `string`                                                                                                                                                                                                                 | :heavy_check_mark:                                                                                                                                                                                                       | N/A                                                                                                                                                                                                                      | 019a8f3e-4b2c-7d1e-9f3a-2c4b6d8e0f11                                                                                                                                                                                     |
| `timeout_`                                                                                                                                                                                                               | `*string`                                                                                                                                                                                                                | :heavy_minus_sign:                                                                                                                                                                                                       | How long to wait for the operation to finish, as seconds with an `s`<br/>suffix (`10s`, `2.5s`). The call returns the operation when it is done or<br/>when the timeout passes, whichever is first; check `done`. At most `60s`. | 10s                                                                                                                                                                                                                      |
| `opts`                                                                                                                                                                                                                   | [][operations.Option](../../models/operations/option.md)                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                                                                       | The options for this request.                                                                                                                                                                                            |                                                                                                                                                                                                                          |

### Response

**[*operations.SpaceOperationsWaitResponse](../../models/operations/spaceoperationswaitresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |