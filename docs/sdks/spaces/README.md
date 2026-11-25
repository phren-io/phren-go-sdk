# Spaces

## Overview

### Available Operations

* [List](#list) - List the spaces in the organization the caller can see.

`filter` takes an AIP-160 expression on `project`, the only field it
supports: `project = "organizations/{organization}/projects/{project}"`
lists that project's spaces. With `include=permissions`, the list's
`create` is known only when `filter` names the project. With
`showDeleted`, it also lists the deleted spaces the caller can undelete.
* [Create](#create) - Create. The project's admins create spaces in it.
* [Get](#get) - Get
* [Delete](#delete) - Soft-delete. The space's admins delete it. The delete runs in the
background: this returns its long-running operation, which
`SpaceOperations` get and `:wait` follow until it is done, with the space
`DELETED`. A deleted space's memories are hidden, and its project's admins
can undelete it.
* [SpacesExport](#spacesexport) - Export the space (RFC 008). The space's exporters can export it: its
admins by default. In one transaction this records which memories the
export holds and closes the returned operation; `SpaceOperations`
`:download` then serves its `phren.space/v1` file, and an import can take
it as `from`.

`phren.space/v1` is JSON Lines: a header (`format`, `space` with
`displayName`, `source`, `exportedAt`, `export`), one line per memory
(`content`, `kind`, `labels`, `source`, `origin` with `name`,
`createdAt`, `createdBy`, `createdWith`, and `verified: false` when the
origin was itself only claimed), and a trailer (`count`, `deleted`,
`sha256`, the hex SHA-256 of the memory lines). Readers ignore fields
they don't know.
* [SpacesImport](#spacesimport) - Import into the space, as its importer: the space's editors can import.
With `from`, an export of this deployment, memory copies the source's
rows, so each memory's `origin` is verified, and a memory already
imported from the same origin is skipped: importing the same export
again adds nothing. `from` also needs `can_export` on the source, and
counts as a download of it. Without `from`, send the file to the
returned operation's `:append`; the import starts at its trailer. A
file's origins are claims (`claimedOrigin`), and a line whose content the
space held before the import is skipped. Each line is one memory: a line
over 32 KiB, a memory's limit, is refused with its line number. One
import runs per organization at a time (409). The operation is done when
the imported memories are searchable (`progress.indexed`).
* [SpacesQuery](#spacesquery) - Search the space's memories. The space's viewers, editors and admins can
query it.
* [Undelete](#undelete) - Undelete. The admins of the space's project undelete it. The restore runs
in the background: this returns its long-running operation, done when the
space is `ACTIVE` again.

## List

List the spaces in the organization the caller can see.

`filter` takes an AIP-160 expression on `project`, the only field it
supports: `project = "organizations/{organization}/projects/{project}"`
lists that project's spaces. With `include=permissions`, the list's
`create` is known only when `filter` names the project. With
`showDeleted`, it also lists the deleted spaces the caller can undelete.

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

## Delete

Soft-delete. The space's admins delete it. The delete runs in the
background: this returns its long-running operation, which
`SpaceOperations` get and `:wait` follow until it is done, with the space
`DELETED`. A deleted space's memories are hidden, and its project's admins
can undelete it.

### Example Usage

<!-- UsageSnippet language="go" operationID="Spaces_delete" method="delete" path="/v1/organizations/{organization}/spaces/{space}" -->
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

    res, err := s.Spaces.Delete(ctx, "acme", "notes")
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
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.SpacesDeleteResponse](../../models/operations/spacesdeleteresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404, 409  | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## SpacesExport

Export the space (RFC 008). The space's exporters can export it: its
admins by default. In one transaction this records which memories the
export holds and closes the returned operation; `SpaceOperations`
`:download` then serves its `phren.space/v1` file, and an import can take
it as `from`.

`phren.space/v1` is JSON Lines: a header (`format`, `space` with
`displayName`, `source`, `exportedAt`, `export`), one line per memory
(`content`, `kind`, `labels`, `source`, `origin` with `name`,
`createdAt`, `createdBy`, `createdWith`, and `verified: false` when the
origin was itself only claimed), and a trailer (`count`, `deleted`,
`sha256`, the hex SHA-256 of the memory lines). Readers ignore fields
they don't know.

### Example Usage

<!-- UsageSnippet language="go" operationID="Spaces_export" method="post" path="/v1/organizations/{organization}/spaces/{space}:export" -->
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

    res, err := s.Spaces.SpacesExport(ctx, "acme", "notes")
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
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.SpacesExportResponse](../../models/operations/spacesexportresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404, 409  | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## SpacesImport

Import into the space, as its importer: the space's editors can import.
With `from`, an export of this deployment, memory copies the source's
rows, so each memory's `origin` is verified, and a memory already
imported from the same origin is skipped: importing the same export
again adds nothing. `from` also needs `can_export` on the source, and
counts as a download of it. Without `from`, send the file to the
returned operation's `:append`; the import starts at its trailer. A
file's origins are claims (`claimedOrigin`), and a line whose content the
space held before the import is skipped. Each line is one memory: a line
over 32 KiB, a memory's limit, is refused with its line number. One
import runs per organization at a time (409). The operation is done when
the imported memories are searchable (`progress.indexed`).

### Example Usage

<!-- UsageSnippet language="go" operationID="Spaces_import" method="post" path="/v1/organizations/{organization}/spaces/{space}:import" -->
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

    res, err := s.Spaces.SpacesImport(ctx, "acme", "handbook", components.ImportSpaceRequest{
        From: phren.Pointer("organizations/acme/spaces/notes/operations/019aa1b2-3c4d-7e5f-8a6b-7c8d9e0f1a33"),
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.SpaceOperation != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                      | Type                                                                           | Required                                                                       | Description                                                                    | Example                                                                        |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ |
| `ctx`                                                                          | [context.Context](https://pkg.go.dev/context#Context)                          | :heavy_check_mark:                                                             | The context to use for the request.                                            |                                                                                |
| `organization`                                                                 | `string`                                                                       | :heavy_check_mark:                                                             | N/A                                                                            | acme                                                                           |
| `space`                                                                        | `string`                                                                       | :heavy_check_mark:                                                             | N/A                                                                            | handbook                                                                       |
| `body`                                                                         | [components.ImportSpaceRequest](../../models/components/importspacerequest.md) | :heavy_check_mark:                                                             | N/A                                                                            |                                                                                |
| `opts`                                                                         | [][operations.Option](../../models/operations/option.md)                       | :heavy_minus_sign:                                                             | The options for this request.                                                  |                                                                                |

### Response

**[*operations.SpacesImportResponse](../../models/operations/spacesimportresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404, 409  | application/problem+json |
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

## Undelete

Undelete. The admins of the space's project undelete it. The restore runs
in the background: this returns its long-running operation, done when the
space is `ACTIVE` again.

### Example Usage

<!-- UsageSnippet language="go" operationID="Spaces_undelete" method="post" path="/v1/organizations/{organization}/spaces/{space}:undelete" -->
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

    res, err := s.Spaces.Undelete(ctx, "acme", "notes")
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
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.SpacesUndeleteResponse](../../models/operations/spacesundeleteresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404, 409  | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |