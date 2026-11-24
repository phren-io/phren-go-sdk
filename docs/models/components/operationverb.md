# OperationVerb

What a long-running operation does to its target.

## Example Usage

```go
import (
	"github.com/phren-io/phren-go-sdk/models/components"
)

value := components.OperationVerbDelete

// Open enum: custom values can be created with a direct type cast
custom := components.OperationVerb("custom_value")
```


## Values

| Name                    | Value                   |
| ----------------------- | ----------------------- |
| `OperationVerbDelete`   | delete                  |
| `OperationVerbUndelete` | undelete                |