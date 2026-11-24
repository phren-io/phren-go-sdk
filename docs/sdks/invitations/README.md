# Invitations

## Overview

### Available Operations

* [List](#list) - List. Admins list an organization's invitations. With `-` as the
organization, lists the pending invitations addressed to the caller's
email, across organizations.
* [Create](#create) - Invite someone by email. Fails with 409 if they're already a member or
already have a pending invitation.
* [Get](#get) - Get
* [Delete](#delete) - Revoke
* [Accept](#accept) - Accept, joining the organization. Only the invitee can accept, while the
invitation is pending and unexpired; otherwise it fails with 409.
* [Decline](#decline) - Decline. Only the invitee can decline, while the invitation is pending.

## List

List. Admins list an organization's invitations. With `-` as the
organization, lists the pending invitations addressed to the caller's
email, across organizations.

### Example Usage: Addressed to me

<!-- UsageSnippet language="go" operationID="Invitations_list" method="get" path="/v1/organizations/{organization}/invitations" example="Addressed to me" -->
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

    res, err := s.Invitations.List(ctx, operations.InvitationsListRequest{
        Organization: "-",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ListInvitationsResponse != nil {
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
### Example Usage: An organization's

<!-- UsageSnippet language="go" operationID="Invitations_list" method="get" path="/v1/organizations/{organization}/invitations" example="An organization's" -->
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

    res, err := s.Invitations.List(ctx, operations.InvitationsListRequest{
        Organization: "acme",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ListInvitationsResponse != nil {
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
| `request`                                                                              | [operations.InvitationsListRequest](../../models/operations/invitationslistrequest.md) | :heavy_check_mark:                                                                     | The request object to use for the request.                                             |
| `opts`                                                                                 | [][operations.Option](../../models/operations/option.md)                               | :heavy_minus_sign:                                                                     | The options for this request.                                                          |

### Response

**[*operations.InvitationsListResponse](../../models/operations/invitationslistresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403            | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Create

Invite someone by email. Fails with 409 if they're already a member or
already have a pending invitation.

### Example Usage

<!-- UsageSnippet language="go" operationID="Invitations_create" method="post" path="/v1/organizations/{organization}/invitations" -->
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

    res, err := s.Invitations.Create(ctx, "acme", components.CreateInvitation{
        Email: "bob@acme.example",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.Invitation != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                | Example                                                                    |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `ctx`                                                                      | [context.Context](https://pkg.go.dev/context#Context)                      | :heavy_check_mark:                                                         | The context to use for the request.                                        |                                                                            |
| `organization`                                                             | `string`                                                                   | :heavy_check_mark:                                                         | N/A                                                                        | acme                                                                       |
| `body`                                                                     | [components.CreateInvitation](../../models/components/createinvitation.md) | :heavy_check_mark:                                                         | N/A                                                                        | {<br/>"email": "bob@acme.example"<br/>}                                    |
| `opts`                                                                     | [][operations.Option](../../models/operations/option.md)                   | :heavy_minus_sign:                                                         | The options for this request.                                              |                                                                            |

### Response

**[*operations.InvitationsCreateResponse](../../models/operations/invitationscreateresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 409       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Get

Get

### Example Usage

<!-- UsageSnippet language="go" operationID="Invitations_get" method="get" path="/v1/organizations/{organization}/invitations/{invitation}" -->
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

    res, err := s.Invitations.Get(ctx, "acme", "0196f1c4-9a2b-7e3d-8f1c-6a7b8c9d0e03", nil)
    if err != nil {
        log.Fatal(err)
    }
    if res.Invitation != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                                                                                                                                                                       | Type                                                                                                                                                                                                                                                            | Required                                                                                                                                                                                                                                                        | Description                                                                                                                                                                                                                                                     | Example                                                                                                                                                                                                                                                         |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ctx`                                                                                                                                                                                                                                                           | [context.Context](https://pkg.go.dev/context#Context)                                                                                                                                                                                                           | :heavy_check_mark:                                                                                                                                                                                                                                              | The context to use for the request.                                                                                                                                                                                                                             |                                                                                                                                                                                                                                                                 |
| `organization`                                                                                                                                                                                                                                                  | `string`                                                                                                                                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                                                              | N/A                                                                                                                                                                                                                                                             | acme                                                                                                                                                                                                                                                            |
| `invitation`                                                                                                                                                                                                                                                    | `string`                                                                                                                                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                                                              | N/A                                                                                                                                                                                                                                                             | 0196f1c4-9a2b-7e3d-8f1c-6a7b8c9d0e03                                                                                                                                                                                                                            |
| `include`                                                                                                                                                                                                                                                       | [*components.Include](../../models/components/include.md)                                                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                                                              | Extra data to return. With `permissions`, each resource lists the methods<br/>the caller may call on it, and a list response the methods on the<br/>collection. Rules that depend on data, such as keeping the last admin, are<br/>still checked when the method is called. |                                                                                                                                                                                                                                                                 |
| `opts`                                                                                                                                                                                                                                                          | [][operations.Option](../../models/operations/option.md)                                                                                                                                                                                                        | :heavy_minus_sign:                                                                                                                                                                                                                                              | The options for this request.                                                                                                                                                                                                                                   |                                                                                                                                                                                                                                                                 |

### Response

**[*operations.InvitationsGetResponse](../../models/operations/invitationsgetresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Delete

Revoke

### Example Usage

<!-- UsageSnippet language="go" operationID="Invitations_delete" method="delete" path="/v1/organizations/{organization}/invitations/{invitation}" -->
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

    res, err := s.Invitations.Delete(ctx, "<value>", "<value>")
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
| `invitation`                                             | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.InvitationsDeleteResponse](../../models/operations/invitationsdeleteresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404, 409  | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Accept

Accept, joining the organization. Only the invitee can accept, while the
invitation is pending and unexpired; otherwise it fails with 409.

### Example Usage

<!-- UsageSnippet language="go" operationID="Invitations_accept" method="post" path="/v1/organizations/{organization}/invitations/{invitation}:accept" -->
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

    res, err := s.Invitations.Accept(ctx, "acme", "0196f1c4-9a2b-7e3d-8f1c-6a7b8c9d0e03")
    if err != nil {
        log.Fatal(err)
    }
    if res.Invitation != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              | Example                                                  |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |                                                          |
| `organization`                                           | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      | acme                                                     |
| `invitation`                                             | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      | 0196f1c4-9a2b-7e3d-8f1c-6a7b8c9d0e03                     |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.InvitationsAcceptResponse](../../models/operations/invitationsacceptresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404, 409  | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Decline

Decline. Only the invitee can decline, while the invitation is pending.

### Example Usage

<!-- UsageSnippet language="go" operationID="Invitations_decline" method="post" path="/v1/organizations/{organization}/invitations/{invitation}:decline" -->
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

    res, err := s.Invitations.Decline(ctx, "acme", "0196f1c4-9a2b-7e3d-8f1c-6a7b8c9d0e03")
    if err != nil {
        log.Fatal(err)
    }
    if res.Invitation != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              | Example                                                  |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |                                                          |
| `organization`                                           | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      | acme                                                     |
| `invitation`                                             | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      | 0196f1c4-9a2b-7e3d-8f1c-6a7b8c9d0e03                     |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.InvitationsDeclineResponse](../../models/operations/invitationsdeclineresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404, 409  | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |