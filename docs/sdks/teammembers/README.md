# TeamMembers

## Overview

### Available Operations

* [List](#list) - List
* [Create](#create) - Add an organization member to the team. Team admins add members; adding
one as an admin needs the right to grant admin. Fails with 409 if they're
already in the team.
* [Get](#get) - Get
* [Delete](#delete) - Remove a member. Team admins remove anyone; members remove themselves.

## List

List

### Example Usage

<!-- UsageSnippet language="go" operationID="TeamMembers_list" method="get" path="/v1/organizations/{organization}/teams/{team}/members" -->
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

    res, err := s.TeamMembers.List(ctx, operations.TeamMembersListRequest{
        Organization: "acme",
        Team: "core",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ListTeamMembersResponse != nil {
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

| Parameter                                                                              | Type                                                                                   | Required                                                                               | Description                                                                            |
| -------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| `ctx`                                                                                  | [context.Context](https://pkg.go.dev/context#Context)                                  | :heavy_check_mark:                                                                     | The context to use for the request.                                                    |
| `request`                                                                              | [operations.TeamMembersListRequest](../../models/operations/teammemberslistrequest.md) | :heavy_check_mark:                                                                     | The request object to use for the request.                                             |
| `opts`                                                                                 | [][operations.Option](../../models/operations/option.md)                               | :heavy_minus_sign:                                                                     | The options for this request.                                                          |

### Response

**[*operations.TeamMembersListResponse](../../models/operations/teammemberslistresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403            | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Create

Add an organization member to the team. Team admins add members; adding
one as an admin needs the right to grant admin. Fails with 409 if they're
already in the team.

### Example Usage

<!-- UsageSnippet language="go" operationID="TeamMembers_create" method="post" path="/v1/organizations/{organization}/teams/{team}/members" -->
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

    res, err := s.TeamMembers.Create(ctx, "acme", "core", components.CreateTeamMember{
        Member: "organizations/acme/members/0196f1b8-2d4f-7a1c-8e3b-5c6d7e8f9a02",
        Roles: []components.MemberRole{
            components.MemberRoleAdmin,
        },
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.TeamMember != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                             | Type                                                                                                  | Required                                                                                              | Description                                                                                           | Example                                                                                               |
| ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| `ctx`                                                                                                 | [context.Context](https://pkg.go.dev/context#Context)                                                 | :heavy_check_mark:                                                                                    | The context to use for the request.                                                                   |                                                                                                       |
| `organization`                                                                                        | `string`                                                                                              | :heavy_check_mark:                                                                                    | N/A                                                                                                   | acme                                                                                                  |
| `team`                                                                                                | `string`                                                                                              | :heavy_check_mark:                                                                                    | N/A                                                                                                   | core                                                                                                  |
| `body`                                                                                                | [components.CreateTeamMember](../../models/components/createteammember.md)                            | :heavy_check_mark:                                                                                    | N/A                                                                                                   | {<br/>"member": "organizations/acme/members/0196f1b8-2d4f-7a1c-8e3b-5c6d7e8f9a02",<br/>"roles": [<br/>"admin"<br/>]<br/>} |
| `opts`                                                                                                | [][operations.Option](../../models/operations/option.md)                                              | :heavy_minus_sign:                                                                                    | The options for this request.                                                                         |                                                                                                       |

### Response

**[*operations.TeamMembersCreateResponse](../../models/operations/teammemberscreateresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 409       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Get

Get

### Example Usage

<!-- UsageSnippet language="go" operationID="TeamMembers_get" method="get" path="/v1/organizations/{organization}/teams/{team}/members/{member}" -->
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

    res, err := s.TeamMembers.Get(ctx, "acme", "core", "0196f1d0-3b4c-7d5e-9f1a-2b3c4d5e6f04")
    if err != nil {
        log.Fatal(err)
    }
    if res.TeamMember != nil {
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
| `member`                                                 | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      | 0196f1d0-3b4c-7d5e-9f1a-2b3c4d5e6f04                     |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.TeamMembersGetResponse](../../models/operations/teammembersgetresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Delete

Remove a member. Team admins remove anyone; members remove themselves.

### Example Usage

<!-- UsageSnippet language="go" operationID="TeamMembers_delete" method="delete" path="/v1/organizations/{organization}/teams/{team}/members/{member}" -->
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

    res, err := s.TeamMembers.Delete(ctx, "<value>", "<value>", "<value>")
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
| `team`                                                   | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `member`                                                 | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.TeamMembersDeleteResponse](../../models/operations/teammembersdeleteresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404, 409  | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |