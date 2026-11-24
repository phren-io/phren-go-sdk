# OrganizationState

Lifecycle state of an organization.

## Example Usage

```go
import (
	"github.com/phren-io/phren-go-sdk/models/components"
)

value := components.OrganizationStateActive

// Open enum: custom values can be created with a direct type cast
custom := components.OrganizationState("custom_value")
```


## Values

| Name                         | Value                        |
| ---------------------------- | ---------------------------- |
| `OrganizationStateActive`    | active                       |
| `OrganizationStateDeleting`  | deleting                     |
| `OrganizationStateDeleted`   | deleted                      |
| `OrganizationStateRestoring` | restoring                    |