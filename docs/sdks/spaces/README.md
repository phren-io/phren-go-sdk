# Spaces

## Overview

### Available Operations

* [List](#list) - List the spaces in the organization the caller can see.

`filter` takes an AIP-160 expression on `project`, the only field it
supports: `project = "organizations/{organization}/projects/{project}"`
lists that project's spaces. With `include=permissions`, the list's
`create` is known only when `filter` names the project.
* [Create](#create) - Create. The project's admins create spaces in it.
* [Get](#get) - Get
* [SpacesQuery](#spacesquery) - Search the space's memories. The space's viewers, editors and admins can
query it.

## List

List the spaces in the organization the caller can see.

`filter` takes an AIP-160 expression on `project`, the only field it
supports: `project = "organizations/{organization}/projects/{project}"`
lists that project's spaces. With `include=permissions`, the list's
`create` is known only when `filter` names the project.

### Example Usage: With permissions

<!-- UsageSnippet language="go" operationID="Spaces_list" method="get" path="/v1/organizations/{organization}/spaces" example="With permissions" -->
```go
package main

import(
	"context"
	"os"
	phren "github.com/phren-io/phren-go-sdk"
	"github.com/phren-io/phren-go-sdk/models/components"
	"github.com/phren-io/phren-go-sdk/models/operations"
	"log"
)

func main() {
    ctx := context.Background()

    s := phren.New(
        phren.WithSecurity(os.Getenv("PHREN_BEARER_AUTH")),
    )

    res, err := s.Spaces.List(ctx, operations.SpacesListRequest{
        Filter: phren.Pointer("project = \"organizations/acme/projects/agent\""),
        Include: components.IncludePermissions.ToPointer(),
        Organization: "acme",
    })
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
### Example Usage: example0

<!-- UsageSnippet language="go" operationID="Spaces_list" method="get" path="/v1/organizations/{organization}/spaces" example="example0" -->
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

    res, err := s.Spaces.List(ctx, operations.SpacesListRequest{
        Filter: phren.Pointer("project = \"organizations/acme/projects/agent\""),
        Organization: "acme",
    })
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
### Example Usage: example1

<!-- UsageSnippet language="go" operationID="Spaces_list" method="get" path="/v1/organizations/{organization}/spaces" example="example1" -->
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

    res, err := s.Spaces.List(ctx, operations.SpacesListRequest{
        Filter: phren.Pointer("project = \"organizations/acme/projects/agent\""),
        Organization: "acme",
    })
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
### Example Usage: example2

<!-- UsageSnippet language="go" operationID="Spaces_list" method="get" path="/v1/organizations/{organization}/spaces" example="example2" -->
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

    res, err := s.Spaces.List(ctx, operations.SpacesListRequest{
        Organization: "acme",
    })
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

| Parameter                                                                    | Type                                                                         | Required                                                                     | Description                                                                  |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `ctx`                                                                        | [context.Context](https://pkg.go.dev/context#Context)                        | :heavy_check_mark:                                                           | The context to use for the request.                                          |
| `request`                                                                    | [operations.SpacesListRequest](../../models/operations/spaceslistrequest.md) | :heavy_check_mark:                                                           | The request object to use for the request.                                   |
| `opts`                                                                       | [][operations.Option](../../models/operations/option.md)                     | :heavy_minus_sign:                                                           | The options for this request.                                                |

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
        Project: "organizations/acme/projects/agent",
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

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                | Example                                                                    |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `ctx`                                                                      | [context.Context](https://pkg.go.dev/context#Context)                      | :heavy_check_mark:                                                         | The context to use for the request.                                        |                                                                            |
| `organization`                                                             | `string`                                                                   | :heavy_check_mark:                                                         | N/A                                                                        | acme                                                                       |
| `spaceID`                                                                  | `string`                                                                   | :heavy_check_mark:                                                         | N/A                                                                        | notes                                                                      |
| `body`                                                                     | [components.CreateSpace](../../models/components/createspace.md)           | :heavy_check_mark:                                                         | N/A                                                                        | {<br/>"project": "organizations/acme/projects/agent",<br/>"displayName": "Notes"<br/>} |
| `opts`                                                                     | [][operations.Option](../../models/operations/option.md)                   | :heavy_minus_sign:                                                         | The options for this request.                                              |                                                                            |

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

    res, err := s.Spaces.Get(ctx, "acme", "notes", nil)
    if err != nil {
        log.Fatal(err)
    }
    if res.Space != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                                                       | Type                                                                                                                                                                                                                                                            | Required                                                                                                                                                                                                                                                        | Description                                                                                                                                                                                                                                                     | Example                                                                                                                                                                                                                                                         |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ctx`                                                                                                                                                                                                                                                           | [context.Context](https://pkg.go.dev/context#Context)                                                                                                                                                                                                           | :heavy_check_mark:                                                                                                                                                                                                                                              | The context to use for the request.                                                                                                                                                                                                                             |                                                                                                                                                                                                                                                                 |
| `organization`                                                                                                                                                                                                                                                  | `string`                                                                                                                                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                                                              | N/A                                                                                                                                                                                                                                                             | acme                                                                                                                                                                                                                                                            |
| `space`                                                                                                                                                                                                                                                         | `string`                                                                                                                                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                                                              | N/A                                                                                                                                                                                                                                                             | notes                                                                                                                                                                                                                                                           |
| `include`                                                                                                                                                                                                                                                       | [*components.Include](../../models/components/include.md)                                                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                                                              | Extra data to return. With `permissions`, each resource lists the methods<br/>the caller may call on it, and a list response the methods on the<br/>collection. Rules that depend on data, such as keeping the last admin, are<br/>still checked when the method is called. |                                                                                                                                                                                                                                                                 |
| `opts`                                                                                                                                                                                                                                                          | [][operations.Option](../../models/operations/option.md)                                                                                                                                                                                                        | :heavy_minus_sign:                                                                                                                                                                                                                                              | The options for this request.                                                                                                                                                                                                                                   |                                                                                                                                                                                                                                                                 |

### Response

**[*operations.SpacesGetResponse](../../models/operations/spacesgetresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## SpacesQuery

Search the space's memories. The space's viewers, editors and admins can
query it.

### Example Usage

<!-- UsageSnippet language="go" operationID="Spaces_query" method="post" path="/v1/organizations/{organization}/spaces/{space}:query" -->
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

    res, err := s.Spaces.SpacesQuery(ctx, "acme", "notes", components.QuerySpaceRequest{
        Query: "How do deploys work?",
        PageSize: phren.Pointer[int](5),
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.QuerySpaceResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                    | Type                                                                         | Required                                                                     | Description                                                                  | Example                                                                      |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `ctx`                                                                        | [context.Context](https://pkg.go.dev/context#Context)                        | :heavy_check_mark:                                                           | The context to use for the request.                                          |                                                                              |
| `organization`                                                               | `string`                                                                     | :heavy_check_mark:                                                           | N/A                                                                          | acme                                                                         |
| `space`                                                                      | `string`                                                                     | :heavy_check_mark:                                                           | N/A                                                                          | notes                                                                        |
| `body`                                                                       | [components.QuerySpaceRequest](../../models/components/queryspacerequest.md) | :heavy_check_mark:                                                           | N/A                                                                          | {<br/>"query": "How do deploys work?",<br/>"pageSize": 5<br/>}               |
| `opts`                                                                       | [][operations.Option](../../models/operations/option.md)                     | :heavy_minus_sign:                                                           | The options for this request.                                                |                                                                              |

### Response

**[*operations.SpacesQueryResponse](../../models/operations/spacesqueryresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404       | application/problem+json |
| apierrors.ProblemError   | 429                      | application/problem+json |
| apierrors.ProblemError   | 503                      | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |