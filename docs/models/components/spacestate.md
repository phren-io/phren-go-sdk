# SpaceState

Lifecycle state of a space.

## Example Usage

```go
import (
	"github.com/phren-io/phren-go-sdk/models/components"
)

value := components.SpaceStateActive

// Open enum: custom values can be created with a direct type cast
custom := components.SpaceState("custom_value")
```


## Values

| Name                  | Value                 |
| --------------------- | --------------------- |
| `SpaceStateActive`    | active                |
| `SpaceStateDeleting`  | deleting              |
| `SpaceStateDeleted`   | deleted               |
| `SpaceStateRestoring` | restoring             |