# InvitationState

Where an invitation stands.

## Example Usage

```go
import (
	"github.com/phren-io/phren-go-sdk/models/components"
)

value := components.InvitationStatePending

// Open enum: custom values can be created with a direct type cast
custom := components.InvitationState("custom_value")
```


## Values

| Name                      | Value                     |
| ------------------------- | ------------------------- |
| `InvitationStatePending`  | pending                   |
| `InvitationStateAccepted` | accepted                  |
| `InvitationStateDeclined` | declined                  |