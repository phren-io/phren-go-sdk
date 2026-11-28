# Sources

## Overview

### Available Operations

* [SpaceSourcesListCandidates](#spacesourceslistcandidates) - List the organization's spaces the space may add as sources: the ones
its project may link, but for itself and its sources. The space's
editors can list them. A page may hold fewer than `pageSize` spaces.
* [List](#list) - List the space's sources. The space's viewers can list them.
* [Create](#create) - Add a source. The space's editors add one, when the space's project may
link the source: the source's own project always may, others when the
source's admins granted it (`linkGrants`).
* [Delete](#delete) - Remove a source. The space's editors remove it, and so do the source's
admins (from its `usedBy`).
* [SpaceSourcesListUsedBy](#spacesourceslistusedby) - List the sources that name this space: who uses it. Its admins can.

## SpaceSourcesListCandidates

List the organization's spaces the space may add as sources: the ones
its project may link, but for itself and its sources. The space's
editors can list them. A page may hold fewer than `pageSize` spaces.

### Example Usage

<!-- UsageSnippet language="go" operationID="SpaceSources_listCandidates" method="get" path="/v1/organizations/{organization}/spaces/{space}/sourceCandidates" -->
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

    res, err := s.Sources.SpaceSourcesListCandidates(ctx, "acme", "style-guide", phren.Pointer[int](50), nil)
    if err != nil {
        log.Fatal(err)
    }
    if res.ListSourceCandidatesResponse != nil {
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
| `space`                                                  | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      | style-guide                                              |
| `pageSize`                                               | `*int`                                                   | :heavy_minus_sign:                                       | Maximum number of results to return.                     | 50                                                       |
| `pageToken`                                              | `*string`                                                | :heavy_minus_sign:                                       | Token from a previous response's nextPageToken.          |                                                          |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.SpaceSourcesListCandidatesResponse](../../models/operations/spacesourceslistcandidatesresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## List

List the space's sources. The space's viewers can list them.

### Example Usage

<!-- UsageSnippet language="go" operationID="SpaceSources_list" method="get" path="/v1/organizations/{organization}/spaces/{space}/sources" -->
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

    res, err := s.Sources.List(ctx, "acme", "notes", phren.Pointer[int](50), nil)
    if err != nil {
        log.Fatal(err)
    }
    if res.ListSpaceSourcesResponse != nil {
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
| `space`                                                  | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      | notes                                                    |
| `pageSize`                                               | `*int`                                                   | :heavy_minus_sign:                                       | Maximum number of results to return.                     | 50                                                       |
| `pageToken`                                              | `*string`                                                | :heavy_minus_sign:                                       | Token from a previous response's nextPageToken.          |                                                          |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.SpaceSourcesListResponse](../../models/operations/spacesourceslistresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Create

Add a source. The space's editors add one, when the space's project may
link the source: the source's own project always may, others when the
source's admins granted it (`linkGrants`).

### Example Usage

<!-- UsageSnippet language="go" operationID="SpaceSources_create" method="post" path="/v1/organizations/{organization}/spaces/{space}/sources" -->
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

    res, err := s.Sources.Create(ctx, "acme", "notes", components.CreateSpaceSource{
        Source: "organizations/acme/spaces/style-guide",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.SpaceSource != nil {
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
| `body`                                                                       | [components.CreateSpaceSource](../../models/components/createspacesource.md) | :heavy_check_mark:                                                           | N/A                                                                          | {<br/>"source": "organizations/acme/spaces/style-guide"<br/>}                |
| `opts`                                                                       | [][operations.Option](../../models/operations/option.md)                     | :heavy_minus_sign:                                                           | The options for this request.                                                |                                                                              |

### Response

**[*operations.SpaceSourcesCreateResponse](../../models/operations/spacesourcescreateresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 409       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## Delete

Remove a source. The space's editors remove it, and so do the source's
admins (from its `usedBy`).

### Example Usage

<!-- UsageSnippet language="go" operationID="SpaceSources_delete" method="delete" path="/v1/organizations/{organization}/spaces/{space}/sources/{source}" -->
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

    res, err := s.Sources.Delete(ctx, "<value>", "<value>", "<value>")
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
| `space`                                                  | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `source`                                                 | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.SpaceSourcesDeleteResponse](../../models/operations/spacesourcesdeleteresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404, 409  | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |

## SpaceSourcesListUsedBy

List the sources that name this space: who uses it. Its admins can.

### Example Usage

<!-- UsageSnippet language="go" operationID="SpaceSources_listUsedBy" method="get" path="/v1/organizations/{organization}/spaces/{space}/usedBy" -->
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

    res, err := s.Sources.SpaceSourcesListUsedBy(ctx, "acme", "style-guide", phren.Pointer[int](50), nil)
    if err != nil {
        log.Fatal(err)
    }
    if res.ListSpaceSourcesResponse != nil {
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
| `space`                                                  | `string`                                                 | :heavy_check_mark:                                       | N/A                                                      | style-guide                                              |
| `pageSize`                                               | `*int`                                                   | :heavy_minus_sign:                                       | Maximum number of results to return.                     | 50                                                       |
| `pageToken`                                              | `*string`                                                | :heavy_minus_sign:                                       | Token from a previous response's nextPageToken.          |                                                          |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.SpaceSourcesListUsedByResponse](../../models/operations/spacesourceslistusedbyresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ProblemError   | 400, 401, 403, 404       | application/problem+json |
| apierrors.APIError       | 4XX, 5XX                 | \*/\*                    |