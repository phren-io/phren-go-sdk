# phren

Developer-friendly & type-safe Go SDK specifically catered to leverage *phren* API.

[![Built by Speakeasy](https://img.shields.io/badge/Built_by-SPEAKEASY-374151?style=for-the-badge&labelColor=f3f4f6)](https://www.speakeasy.com/?utm_source=phren&utm_campaign=go)
[![License: MIT](https://img.shields.io/badge/LICENSE_//_MIT-3b5bdb?style=for-the-badge&labelColor=eff6ff)](https://opensource.org/licenses/MIT)


<br /><br />
> [!IMPORTANT]
> This SDK is not yet ready for production use. To complete setup please follow the steps outlined in your [workspace](https://app.speakeasy.com/org/phren/me). Delete this section before > publishing to a package manager.

<!-- Start Summary [summary] -->
## Summary


<!-- End Summary [summary] -->

<!-- Start Table of Contents [toc] -->
## Table of Contents
<!-- $toc-max-depth=2 -->
* [phren](#phren)
  * [SDK Installation](#sdk-installation)
  * [SDK Example Usage](#sdk-example-usage)
  * [Authentication](#authentication)
  * [Available Resources and Operations](#available-resources-and-operations)
  * [Pagination](#pagination)
  * [Retries](#retries)
  * [Error Handling](#error-handling)
  * [Server Selection](#server-selection)
  * [Custom HTTP Client](#custom-http-client)
* [Development](#development)
  * [Maturity](#maturity)
  * [Contributions](#contributions)

<!-- End Table of Contents [toc] -->

<!-- Start SDK Installation [installation] -->
## SDK Installation

To add the SDK as a dependency to your project:
```bash
go get github.com/phren-io/phren-go-sdk
```
<!-- End SDK Installation [installation] -->

<!-- Start SDK Example Usage [usage] -->
## SDK Example Usage

### Example

```go
package main

import (
	"context"
	phren "github.com/phren-io/phren-go-sdk"
	"github.com/phren-io/phren-go-sdk/models/operations"
	"log"
	"os"
)

func main() {
	ctx := context.Background()

	s := phren.New(
		phren.WithSecurity(os.Getenv("PHREN_BEARER_AUTH")),
	)

	res, err := s.Organizations.List(ctx, operations.OrganizationsListRequest{
		PageToken: phren.Pointer("CiAKGjBpNDd2Nmp2"),
		Filter:    phren.Pointer("state = \"ACTIVE\""),
	})
	if err != nil {
		log.Fatal(err)
	}
	if res.ListOrganizationsResponse != nil {
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
<!-- End SDK Example Usage [usage] -->

<!-- Start Authentication [security] -->
## Authentication

### Per-Client Security Schemes

This SDK supports the following security scheme globally:

| Name         | Type | Scheme      | Environment Variable |
| ------------ | ---- | ----------- | -------------------- |
| `BearerAuth` | http | HTTP Bearer | `PHREN_BEARER_AUTH`  |

You can configure it using the `WithSecurity` option when initializing the SDK client instance. For example:
```go
package main

import (
	"context"
	phren "github.com/phren-io/phren-go-sdk"
	"github.com/phren-io/phren-go-sdk/models/operations"
	"log"
	"os"
)

func main() {
	ctx := context.Background()

	s := phren.New(
		phren.WithSecurity(os.Getenv("PHREN_BEARER_AUTH")),
	)

	res, err := s.Organizations.List(ctx, operations.OrganizationsListRequest{
		PageToken: phren.Pointer("CiAKGjBpNDd2Nmp2"),
		Filter:    phren.Pointer("state = \"ACTIVE\""),
	})
	if err != nil {
		log.Fatal(err)
	}
	if res.ListOrganizationsResponse != nil {
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
<!-- End Authentication [security] -->

<!-- Start Available Resources and Operations [operations] -->
## Available Resources and Operations

<details open>
<summary>Available methods</summary>

### [Invitations](docs/sdks/invitations/README.md)

* [List](docs/sdks/invitations/README.md#list) - List. Admins list an organization's invitations. With `-` as the
organization, lists the pending invitations addressed to the caller's
email, across organizations.
* [Create](docs/sdks/invitations/README.md#create) - Invite someone by email. Fails with 409 if they're already a member or
already have a pending invitation.
* [Get](docs/sdks/invitations/README.md#get) - Get
* [Delete](docs/sdks/invitations/README.md#delete) - Revoke
* [Accept](docs/sdks/invitations/README.md#accept) - Accept, joining the organization. Only the invitee can accept, while the
invitation is pending and unexpired; otherwise it fails with 409.
* [Decline](docs/sdks/invitations/README.md#decline) - Decline. Only the invitee can decline, while the invitation is pending.

### [Members](docs/sdks/members/README.md)

* [List](docs/sdks/members/README.md#list) - List
* [Get](docs/sdks/members/README.md#get) - Get
* [Delete](docs/sdks/members/README.md#delete) - Remove a member. Admins remove anyone, and members remove themselves to
leave. Removing the organization's last admin fails with 409.

### [Memories](docs/sdks/memories/README.md)

* [List](docs/sdks/memories/README.md#list) - List, newest first.
* [Create](docs/sdks/memories/README.md#create) - Create. The space's editors create memories.

A create retried with the same `requestId` returns the memory the first
attempt created instead of creating another, for as long as that memory
exists. Reusing a `requestId` for a different memory (content, kind,
labels or source) is a 409.
* [Get](docs/sdks/memories/README.md#get) - Get
* [Delete](docs/sdks/memories/README.md#delete) - Delete. Its vectors are removed from the space in the background.

### [OrganizationOperations](docs/sdks/organizationoperations/README.md)

* [List](docs/sdks/organizationoperations/README.md#list) - List, newest first.
* [Get](docs/sdks/organizationoperations/README.md#get) - Get
* [Cancel](docs/sdks/organizationoperations/README.md#cancel) - Cancel a delete in flight: the delete stops, its operation is done with a
`Cancelled` error, and a new undelete operation restores the
organization. Returns that undelete operation. Fails with 409 if the
operation has already finished (undelete the organization instead) or is
not a delete. Only admins can cancel.
* [Wait](docs/sdks/organizationoperations/README.md#wait) - Wait for the operation to finish. Returns it when it is done or when
`timeout` passes, whichever is first; check `done` and call again if it
is still running.

### [Organizations](docs/sdks/organizations/README.md)

* [List](docs/sdks/organizations/README.md#list) - List
* [Create](docs/sdks/organizations/README.md#create) - Create
* [Get](docs/sdks/organizations/README.md#get) - Get
* [Delete](docs/sdks/organizations/README.md#delete) - Soft-delete. The delete runs in the background: this returns its
long-running operation, which `OrganizationOperations` get and `:wait`
follow until it is done, with the organization `DELETED`.
* [Undelete](docs/sdks/organizations/README.md#undelete) - Undelete. The restore runs in the background: this returns its
long-running operation, done when the organization is `ACTIVE` again.

### [ProjectMembers](docs/sdks/projectmembers/README.md)

* [List](docs/sdks/projectmembers/README.md#list) - List. The project's members can list them.
* [Create](docs/sdks/projectmembers/README.md#create) - Add an organization member to the project. Project admins add members; adding
one as an admin needs the right to grant admin. Fails with 409 if they're
already in the project.
* [Get](docs/sdks/projectmembers/README.md#get) - Get
* [Delete](docs/sdks/projectmembers/README.md#delete) - Remove a member. Project admins remove anyone; members remove themselves.

### [Projects](docs/sdks/projects/README.md)

* [List](docs/sdks/projects/README.md#list) - List the projects in the organization the caller is a member of.
Organization admins see every project.
* [Create](docs/sdks/projects/README.md#create) - Create. Organization admins create projects, and manage them without
joining: add a member as the project's admin to hand it over.
* [Get](docs/sdks/projects/README.md#get) - Get

### [SpaceOperations](docs/sdks/spaceoperations/README.md)

* [List](docs/sdks/spaceoperations/README.md#list) - List, newest first.
* [Get](docs/sdks/spaceoperations/README.md#get) - Get
* [SpaceOperationsAppend](docs/sdks/spaceoperations/README.md#spaceoperationsappend) - Append a piece of a `phren.space/v1` file to an import started without
`from`: at most 100 lines and 120,000 bytes, the header first and the
trailer last. The trailer's count and SHA-256 are checked against every
line received, and the import starts. Only the person and agent that
started the import may append.
* [Cancel](docs/sdks/spaceoperations/README.md#cancel) - Cancel a delete in flight: the delete stops, its operation is done with a
`Cancelled` error, and a new undelete operation restores the space.
Returns that undelete operation. Fails with 409 if the operation has
already finished (undelete the space instead) or is not a delete. The
admins of the space's project can cancel.
* [SpaceOperationsDownload](docs/sdks/spaceoperations/README.md#spaceoperationsdownload) - Download an export's `phren.space/v1` file: the memories it holds that
still exist. Fails with 409 if the operation is not an export. The
space's exporters can download it; each download is recorded and
publishes `space.exported`.
* [Wait](docs/sdks/spaceoperations/README.md#wait) - Wait for the operation to finish. Returns it when it is done or when
`timeout` passes, whichever is first; check `done` and call again if it
is still running.

### [Spaces](docs/sdks/spaces/README.md)

* [List](docs/sdks/spaces/README.md#list) - List the spaces in the organization the caller can see.

`filter` takes an AIP-160 expression on `project`, the only field it
supports: `project = "organizations/{organization}/projects/{project}"`
lists that project's spaces. With `include=permissions`, the list's
`create` is known only when `filter` names the project. With
`showDeleted`, it also lists the deleted spaces the caller can undelete.
* [Create](docs/sdks/spaces/README.md#create) - Create. The project's admins create spaces in it.
* [Get](docs/sdks/spaces/README.md#get) - Get
* [Delete](docs/sdks/spaces/README.md#delete) - Soft-delete. The space's admins delete it. The delete runs in the
background: this returns its long-running operation, which
`SpaceOperations` get and `:wait` follow until it is done, with the space
`DELETED`. A deleted space's memories are hidden, and its project's admins
can undelete it.
* [SpacesExport](docs/sdks/spaces/README.md#spacesexport) - Export the space (RFC 008). The space's exporters can export it: its
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
* [SpacesImport](docs/sdks/spaces/README.md#spacesimport) - Import into the space, as its importer: the space's editors can import.
With `from`, an export of this deployment, memory copies the source's
rows, so each memory's `origin` is verified, and a memory already
imported from the same origin is skipped: importing the same export
again adds nothing. `from` also needs `can_export` on the source, and
counts as a download of it. Without `from`, send the file to the
returned operation's `:append`; the import starts at its trailer. A
file's origins are claims (`claimedOrigin`), and a line whose content the
space held before the import is skipped. A line over 32 KiB is split on
paragraph boundaries into numbered parts. One import runs per
organization at a time (409).
* [SpacesQuery](docs/sdks/spaces/README.md#spacesquery) - Search the space's memories. The space's viewers, editors and admins can
query it.
* [Undelete](docs/sdks/spaces/README.md#undelete) - Undelete. The admins of the space's project undelete it. The restore runs
in the background: this returns its long-running operation, done when the
space is `ACTIVE` again.

</details>
<!-- End Available Resources and Operations [operations] -->

<!-- Start Pagination [pagination] -->
## Pagination

Some of the endpoints in this SDK support pagination. To use pagination, you make your SDK calls as usual, but the
returned response object will have a `Next` method that can be called to pull down the next group of results. If the
return value of `Next` is `nil`, then there are no more pages to be fetched.

Here's an example of one such pagination call:
```go
package main

import (
	"context"
	phren "github.com/phren-io/phren-go-sdk"
	"github.com/phren-io/phren-go-sdk/models/operations"
	"log"
	"os"
)

func main() {
	ctx := context.Background()

	s := phren.New(
		phren.WithSecurity(os.Getenv("PHREN_BEARER_AUTH")),
	)

	res, err := s.Organizations.List(ctx, operations.OrganizationsListRequest{
		PageToken: phren.Pointer("CiAKGjBpNDd2Nmp2"),
		Filter:    phren.Pointer("state = \"ACTIVE\""),
	})
	if err != nil {
		log.Fatal(err)
	}
	if res.ListOrganizationsResponse != nil {
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
<!-- End Pagination [pagination] -->

<!-- Start Retries [retries] -->
## Retries

Some of the endpoints in this SDK support retries. If you use the SDK without any configuration, it will fall back to the default retry strategy provided by the API. However, the default retry strategy can be overridden on a per-operation basis, or across the entire SDK.

To change the default retry strategy for a single API call, simply provide a `retry.Config` object to the call by using the `WithRetries` option:
```go
package main

import (
	"context"
	phren "github.com/phren-io/phren-go-sdk"
	"github.com/phren-io/phren-go-sdk/models/operations"
	"github.com/phren-io/phren-go-sdk/retry"
	"log"
	"models/operations"
	"os"
)

func main() {
	ctx := context.Background()

	s := phren.New(
		phren.WithSecurity(os.Getenv("PHREN_BEARER_AUTH")),
	)

	res, err := s.Organizations.List(ctx, operations.OrganizationsListRequest{
		PageToken: phren.Pointer("CiAKGjBpNDd2Nmp2"),
		Filter:    phren.Pointer("state = \"ACTIVE\""),
	}, operations.WithRetries(
		retry.Config{
			Strategy: "backoff",
			Backoff: &retry.BackoffStrategy{
				InitialInterval: 1,
				MaxInterval:     50,
				Exponent:        1.1,
				MaxElapsedTime:  100,
			},
			RetryConnectionErrors: false,
		}))
	if err != nil {
		log.Fatal(err)
	}
	if res.ListOrganizationsResponse != nil {
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

If you'd like to override the default retry strategy for all operations that support retries, you can use the `WithRetryConfig` option at SDK initialization:
```go
package main

import (
	"context"
	phren "github.com/phren-io/phren-go-sdk"
	"github.com/phren-io/phren-go-sdk/models/operations"
	"github.com/phren-io/phren-go-sdk/retry"
	"log"
	"os"
)

func main() {
	ctx := context.Background()

	s := phren.New(
		phren.WithRetryConfig(
			retry.Config{
				Strategy: "backoff",
				Backoff: &retry.BackoffStrategy{
					InitialInterval: 1,
					MaxInterval:     50,
					Exponent:        1.1,
					MaxElapsedTime:  100,
				},
				RetryConnectionErrors: false,
			}),
		phren.WithSecurity(os.Getenv("PHREN_BEARER_AUTH")),
	)

	res, err := s.Organizations.List(ctx, operations.OrganizationsListRequest{
		PageToken: phren.Pointer("CiAKGjBpNDd2Nmp2"),
		Filter:    phren.Pointer("state = \"ACTIVE\""),
	})
	if err != nil {
		log.Fatal(err)
	}
	if res.ListOrganizationsResponse != nil {
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
<!-- End Retries [retries] -->

<!-- Start Error Handling [errors] -->
## Error Handling

Handling errors in this SDK should largely match your expectations. All operations return a response object or an error, they will never return both.

By Default, an API error will return `apierrors.APIError`. When custom error responses are specified for an operation, the SDK may also return their associated error. You can refer to respective *Errors* tables in SDK docs for more details on possible error types for each operation.

For example, the `List` function may return the following errors:

| Error Type             | Status Code   | Content Type             |
| ---------------------- | ------------- | ------------------------ |
| apierrors.ProblemError | 400, 401, 403 | application/problem+json |
| apierrors.APIError     | 4XX, 5XX      | \*/\*                    |

### Example

```go
package main

import (
	"context"
	"errors"
	phren "github.com/phren-io/phren-go-sdk"
	"github.com/phren-io/phren-go-sdk/models/apierrors"
	"github.com/phren-io/phren-go-sdk/models/operations"
	"log"
	"os"
)

func main() {
	ctx := context.Background()

	s := phren.New(
		phren.WithSecurity(os.Getenv("PHREN_BEARER_AUTH")),
	)

	res, err := s.Organizations.List(ctx, operations.OrganizationsListRequest{
		PageToken: phren.Pointer("CiAKGjBpNDd2Nmp2"),
		Filter:    phren.Pointer("state = \"ACTIVE\""),
	})
	if err != nil {

		var e *apierrors.ProblemError
		if errors.As(err, &e) {
			// handle error
			log.Fatal(e.Error())
		}

		var e *apierrors.APIError
		if errors.As(err, &e) {
			// handle error
			log.Fatal(e.Error())
		}
	}
}

```
<!-- End Error Handling [errors] -->

<!-- Start Server Selection [server] -->
## Server Selection

### Select Server by Index

You can override the default server globally using the `WithServerIndex(serverIndex int)` option when initializing the SDK client instance. The selected server will then be used as the default on the operations that use it. This table lists the indexes associated with the available servers:

| #   | Server                         | Description           |
| --- | ------------------------------ | --------------------- |
| 0   | `https://api.phren.io`         | The production server |
| 1   | `https://staging.api.phren.io` | The staging server    |

#### Example

```go
package main

import (
	"context"
	phren "github.com/phren-io/phren-go-sdk"
	"github.com/phren-io/phren-go-sdk/models/operations"
	"log"
	"os"
)

func main() {
	ctx := context.Background()

	s := phren.New(
		phren.WithServerIndex(0),
		phren.WithSecurity(os.Getenv("PHREN_BEARER_AUTH")),
	)

	res, err := s.Organizations.List(ctx, operations.OrganizationsListRequest{
		PageToken: phren.Pointer("CiAKGjBpNDd2Nmp2"),
		Filter:    phren.Pointer("state = \"ACTIVE\""),
	})
	if err != nil {
		log.Fatal(err)
	}
	if res.ListOrganizationsResponse != nil {
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

### Override Server URL Per-Client

The default server can also be overridden globally using the `WithServerURL(serverURL string)` option when initializing the SDK client instance. For example:
```go
package main

import (
	"context"
	phren "github.com/phren-io/phren-go-sdk"
	"github.com/phren-io/phren-go-sdk/models/operations"
	"log"
	"os"
)

func main() {
	ctx := context.Background()

	s := phren.New(
		phren.WithServerURL("https://staging.api.phren.io"),
		phren.WithSecurity(os.Getenv("PHREN_BEARER_AUTH")),
	)

	res, err := s.Organizations.List(ctx, operations.OrganizationsListRequest{
		PageToken: phren.Pointer("CiAKGjBpNDd2Nmp2"),
		Filter:    phren.Pointer("state = \"ACTIVE\""),
	})
	if err != nil {
		log.Fatal(err)
	}
	if res.ListOrganizationsResponse != nil {
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
<!-- End Server Selection [server] -->

<!-- Start Custom HTTP Client [http-client] -->
## Custom HTTP Client

The Go SDK makes API calls that wrap an internal HTTP client. The requirements for the HTTP client are very simple. It must match this interface:

```go
type HTTPClient interface {
	Do(req *http.Request) (*http.Response, error)
}
```

The built-in `net/http` client satisfies this interface and a default client based on the built-in is provided by default. To replace this default with a client of your own, you can implement this interface yourself or provide your own client configured as desired. Here's a simple example, which adds a client with a 30 second timeout.

```go
import (
	"net/http"
	"time"

	"github.com/phren-io/phren-go-sdk"
)

var (
	httpClient = &http.Client{Timeout: 30 * time.Second}
	sdkClient  = phren.New(phren.WithClient(httpClient))
)
```

This can be a convenient way to configure timeouts, cookies, proxies, custom headers, and other low-level configuration.
<!-- End Custom HTTP Client [http-client] -->

<!-- Placeholder for Future Speakeasy SDK Sections -->

# Development

## Maturity

This SDK is in beta, and there may be breaking changes between versions without a major version update. Therefore, we recommend pinning usage
to a specific package version. This way, you can install the same version each time without breaking changes unless you are intentionally
looking for the latest version.

## Contributions

While we value open-source contributions to this SDK, this library is generated programmatically. Any manual changes added to internal files will be overwritten on the next generation. 
We look forward to hearing your feedback. Feel free to open a PR or an issue with a proof of concept and we'll do our best to include it in a future release. 

### SDK Created by [Speakeasy](https://www.speakeasy.com/?utm_source=phren&utm_campaign=go)
