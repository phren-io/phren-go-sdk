# ProjectMembers

## Overview

### Available Operations

* [List](#list) - List. The project's members can list them.
* [Create](#create) - Add an organization member to the project. Project admins add members; adding
one as an admin needs the right to grant admin. Fails with 409 if they're
already in the project.
* [Get](#get) - Get
* [ProjectMembersUpdate](#projectmembersupdate) - Change a member's roles in the project. Making someone an admin needs the
right to grant admin, and making an admin a plain member the right to
revoke it. Demoting the project's last admin fails with 409.
* [Delete](#delete) - Remove a member. Project admins remove anyone; members remove themselves.

## List

List. The project's members can list them.

### Example Usage

<!-- UsageSnippet language="go" operationID="ProjectMembers_list" method="get" path="/v1/organizations/{organization}/projects/{project}/members" -->
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

    res, err := s.ProjectMembers.List(ctx, operations.ProjectMembersListRequest{
        Organization: "acme",
        Project: "agent",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ListProjectMembersResponse != nil {
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

| Parameter                                                                                    | Type                                                                                         | Required                                                                                     | Description                                                                                  |
| -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| `ctx`                                                                                        | [context.Context](https://pkg.go.dev/context#Context)                                        | :heavy_check_mark:                                                                           | The context to use for the request.                                                          |
| `request`                                                                                    | [operations.ProjectMembersListRequest](../../models/operations/projectmemberslistrequest.md) | :heavy_check_mark:                                                                           | The request object to use for the request.                                                   |
| `opts`                                                                                       | [][operations.Option](../../models/operations/option.md)                                     | :heavy_minus_sign:                                                                           | The options for this request.                                                                |

### Response

**[*operations.ProjectMembersListResponse](../../models/operations/projectmemberslistresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403            | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Create

Add an organization member to the project. Project admins add members; adding
one as an admin needs the right to grant admin. Fails with 409 if they're
already in the project.

### Example Usage

<!-- UsageSnippet language="go" operationID="ProjectMembers_create" method="post" path="/v1/organizations/{organization}/projects/{project}/members" -->
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

    res, err := s.ProjectMembers.Create(ctx, "acme", "agent", components.CreateProjectMember{
        Member: "organizations/acme/members/0196f1b8-2d4f-7a1c-8e3b-5c6d7e8f9a02",
        Roles: []components.MemberRole{
            components.MemberRoleAdmin,
        },
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ProjectMember != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                             | Type                                                                                                  | Required                                                                                              | Description                                                                                           | Example                                                                                               |
| ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| `ctx`                                                                                                 | [context.Context](https://pkg.go.dev/context#Context)                                                 | :heavy_check_mark:                                                                                    | The context to use for the request.                                                                   |                                                                                                       |
| `organization`                                                                                        | `string`                                                                                              | :heavy_check_mark:                                                                                    | N/A                                                                                                   | acme                                                                                                  |
| `project`                                                                                             | `string`                                                                                              | :heavy_check_mark:                                                                                    | N/A                                                                                                   | agent                                                                                                 |
| `body`                                                                                                | [components.CreateProjectMember](../../models/components/createprojectmember.md)                      | :heavy_check_mark:                                                                                    | N/A                                                                                                   | {<br/>"member": "organizations/acme/members/0196f1b8-2d4f-7a1c-8e3b-5c6d7e8f9a02",<br/>"roles": [<br/>"admin"<br/>]<br/>} |
| `opts`                                                                                                | [][operations.Option](../../models/operations/option.md)                                              | :heavy_minus_sign:                                                                                    | The options for this request.                                                                         |                                                                                                       |

### Response

**[*operations.ProjectMembersCreateResponse](../../models/operations/projectmemberscreateresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 409       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Get

Get

### Example Usage

<!-- UsageSnippet language="go" operationID="ProjectMembers_get" method="get" path="/v1/organizations/{organization}/projects/{project}/members/{member}" -->
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

    res, err := s.ProjectMembers.Get(ctx, "acme", "agent", "0196f1d0-3b4c-7d5e-9f1a-2b3c4d5e6f04", nil)
    if err != nil {
        log.Fatal(err)
    }
    if res.ProjectMember != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                                                       | Type                                                                                                                                                                                                                                                            | Required                                                                                                                                                                                                                                                        | Description                                                                                                                                                                                                                                                     | Example                                                                                                                                                                                                                                                         |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ctx`                                                                                                                                                                                                                                                           | [context.Context](https://pkg.go.dev/context#Context)                                                                                                                                                                                                           | :heavy_check_mark:                                                                                                                                                                                                                                              | The context to use for the request.                                                                                                                                                                                                                             |                                                                                                                                                                                                                                                                 |
| `organization`                                                                                                                                                                                                                                                  | `string`                                                                                                                                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                                                              | N/A                                                                                                                                                                                                                                                             | acme                                                                                                                                                                                                                                                            |
| `project`                                                                                                                                                                                                                                                       | `string`                                                                                                                                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                                                              | N/A                                                                                                                                                                                                                                                             | agent                                                                                                                                                                                                                                                           |
| `member`                                                                                                                                                                                                                                                        | `string`                                                                                                                                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                                                              | N/A                                                                                                                                                                                                                                                             | 0196f1d0-3b4c-7d5e-9f1a-2b3c4d5e6f04                                                                                                                                                                                                                            |
| `include`                                                                                                                                                                                                                                                       | [*components.Include](../../models/components/include.md)                                                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                                                              | Extra data to return. With `permissions`, each resource lists the methods<br/>the caller may call on it, and a list response the methods on the<br/>collection. Rules that depend on data, such as keeping the last admin, are<br/>still checked when the method is called. |                                                                                                                                                                                                                                                                 |
| `opts`                                                                                                                                                                                                                                                          | [][operations.Option](../../models/operations/option.md)                                                                                                                                                                                                        | :heavy_minus_sign:                                                                                                                                                                                                                                              | The options for this request.                                                                                                                                                                                                                                   |                                                                                                                                                                                                                                                                 |

### Response

**[*operations.ProjectMembersGetResponse](../../models/operations/projectmembersgetresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## ProjectMembersUpdate

Change a member's roles in the project. Making someone an admin needs the
right to grant admin, and making an admin a plain member the right to
revoke it. Demoting the project's last admin fails with 409.

### Example Usage

<!-- UsageSnippet language="go" operationID="ProjectMembers_update" method="patch" path="/v1/organizations/{organization}/projects/{project}/members/{member}" -->
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

    res, err := s.ProjectMembers.ProjectMembersUpdate(ctx, "acme", "agent", "0196f1d0-3b4c-7d5e-9f1a-2b3c4d5e6f04", components.MemberUpdate{
        Roles: []components.MemberRole{
            components.MemberRoleAdmin,
        },
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ProjectMember != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                          | Type                                                               | Required                                                           | Description                                                        | Example                                                            |
| ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ |
| `ctx`                                                              | [context.Context](https://pkg.go.dev/context#Context)              | :heavy_check_mark:                                                 | The context to use for the request.                                |                                                                    |
| `organization`                                                     | `string`                                                           | :heavy_check_mark:                                                 | N/A                                                                | acme                                                               |
| `project`                                                          | `string`                                                           | :heavy_check_mark:                                                 | N/A                                                                | agent                                                              |
| `member`                                                           | `string`                                                           | :heavy_check_mark:                                                 | N/A                                                                | 0196f1d0-3b4c-7d5e-9f1a-2b3c4d5e6f04                               |
| `body`                                                             | [components.MemberUpdate](../../models/components/memberupdate.md) | :heavy_check_mark:                                                 | N/A                                                                |                                                                    |
| `opts`                                                             | [][operations.Option](../../models/operations/option.md)           | :heavy_minus_sign:                                                 | The options for this request.                                      |                                                                    |

### Response

**[*operations.ProjectMembersUpdateResponse](../../models/operations/projectmembersupdateresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404, 409  | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Delete

Remove a member. Project admins remove anyone; members remove themselves.

### Example Usage

<!-- UsageSnippet language="go" operationID="ProjectMembers_delete" method="delete" path="/v1/organizations/{organization}/projects/{project}/members/{member}" -->
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

    res, err := s.ProjectMembers.Delete(ctx, "<value>", "<value>", "<value>")
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
| `project`                                                | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `member`                                                 | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.ProjectMembersDeleteResponse](../../models/operations/projectmembersdeleteresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404, 409  | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |