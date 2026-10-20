# OrganizationState

## Example Usage

```go
import (
	"github.com/phren-io/phren-go-sdk/models/components"
)

value := components.OrganizationStateStateUnspecified

// Open enum: custom values can be created with a direct type cast
custom := components.OrganizationState("custom_value")
```


## Values

| Name                                | Value                               |
| ----------------------------------- | ----------------------------------- |
| `OrganizationStateStateUnspecified` | STATE_UNSPECIFIED                   |
| `OrganizationStateActive`           | ACTIVE                              |
| `OrganizationStateDeleting`         | DELETING                            |
| `OrganizationStateRestoring`        | RESTORING                           |
| `OrganizationStatePurging`          | PURGING                             |
| `OrganizationStateFailed`           | FAILED                              |