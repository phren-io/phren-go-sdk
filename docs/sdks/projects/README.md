# Projects

## Overview

### Available Operations

* [List](#list) - List. The team's members can list its projects.
* [Create](#create) - Create. Team admins create projects.
* [Get](#get) - Get

## List

List. The team's members can list its projects.

### Example Usage

<!-- UsageSnippet language="go" operationID="Projects_list" method="get" path="/v1/organizations/{organization}/teams/{team}/projects" -->
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

    res, err := s.Projects.List(ctx, operations.ProjectsListRequest{
        Organization: "acme",
        Team: "core",
    })
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

| Parameter                                                                        | Type                                                                             | Required                                                                         | Description                                                                      |
| -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `ctx`                                                                            | [context.Context](https://pkg.go.dev/context#Context)                            | :heavy_check_mark:                                                               | The context to use for the request.                                              |
| `request`                                                                        | [operations.ProjectsListRequest](../../models/operations/projectslistrequest.md) | :heavy_check_mark:                                                               | The request object to use for the request.                                       |
| `opts`                                                                           | [][operations.Option](../../models/operations/option.md)                         | :heavy_minus_sign:                                                               | The options for this request.                                                    |

### Response

**[*operations.ProjectsListResponse](../../models/operations/projectslistresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403            | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Create

Create. Team admins create projects.

### Example Usage

<!-- UsageSnippet language="go" operationID="Projects_create" method="post" path="/v1/organizations/{organization}/teams/{team}/projects" -->
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

    res, err := s.Projects.Create(ctx, "acme", "core", "agent", components.CreateProject{
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
| `team`                                                               | `string`                                                             | :heavy_check_mark:                                                   | N/A                                                                  | core                                                                 |
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

<!-- UsageSnippet language="go" operationID="Projects_get" method="get" path="/v1/organizations/{organization}/teams/{team}/projects/{project}" -->
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

    res, err := s.Projects.Get(ctx, "acme", "core", "agent")
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
| `team`                                                   | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      | core                                                     |
| `project`                                                | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      | agent                                                    |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.ProjectsGetResponse](../../models/operations/projectsgetresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |