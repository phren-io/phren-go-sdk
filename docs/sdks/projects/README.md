# Projects

## Overview

### Available Operations

* [List](#list) - List the projects in the organization the caller is a member of.
Organization admins see every project.
* [Create](#create) - Create. Organization admins create projects, and manage them without
joining: add a member as the project's admin to hand it over.
* [Get](#get) - Get

## List

List the projects in the organization the caller is a member of.
Organization admins see every project.

### Example Usage

<!-- UsageSnippet language="go" operationID="Projects_list" method="get" path="/v1/organizations/{organization}/projects" -->
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

    res, err := s.Projects.List(ctx, "acme", phren.Pointer[int](50), nil, nil)
    if err != nil {
        log.Fatal(err)
    }
    if res.ListProjectsResponse != nil {
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

**[*operations.ProjectsListResponse](../../models/operations/projectslistresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403            | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Create

Create. Organization admins create projects, and manage them without
joining: add a member as the project's admin to hand it over.

### Example Usage

<!-- UsageSnippet language="go" operationID="Projects_create" method="post" path="/v1/organizations/{organization}/projects" -->
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

    res, err := s.Projects.Create(ctx, "acme", "agent", components.CreateProject{
        DisplayName: "Agent",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.Project != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                            | Type                                                                 | Required                                                             | Description                                                          | Example                                                              |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `ctx`                                                                | [context.Context](https://pkg.go.dev/context#Context)                | :heavy_check_mark:                                                   | The context to use for the request.                                  |                                                                      |
| `organization`                                                       | `string`                                                             | :heavy_check_mark:                                                   | N/A                                                                  | acme                                                                 |
| `projectID`                                                          | `string`                                                             | :heavy_check_mark:                                                   | N/A                                                                  | agent                                                                |
| `body`                                                               | [components.CreateProject](../../models/components/createproject.md) | :heavy_check_mark:                                                   | N/A                                                                  | {<br/>"displayName": "Agent"<br/>}                                   |
| `opts`                                                               | [][operations.Option](../../models/operations/option.md)             | :heavy_minus_sign:                                                   | The options for this request.                                        |                                                                      |

### Response

**[*operations.ProjectsCreateResponse](../../models/operations/projectscreateresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 409       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Get

Get

### Example Usage

<!-- UsageSnippet language="go" operationID="Projects_get" method="get" path="/v1/organizations/{organization}/projects/{project}" -->
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

    res, err := s.Projects.Get(ctx, "acme", "agent")
    if err != nil {
        log.Fatal(err)
    }
    if res.Project != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              | Example                                                  |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |                                                          |
| `organization`                                           | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      | acme                                                     |
| `project`                                                | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      | agent                                                    |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.ProjectsGetResponse](../../models/operations/projectsgetresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |