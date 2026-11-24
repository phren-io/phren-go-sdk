# MemoryKind

What a memory is, so an agent can tell a quote from the person's own thought
without guessing from the wording. The set is closed: queries filter on it.

## Example Usage

```go
import (
	"github.com/phren-io/phren-go-sdk/models/components"
)

value := components.MemoryKindNote

// Open enum: custom values can be created with a direct type cast
custom := components.MemoryKind("custom_value")
```


## Values

| Name                | Value               |
| ------------------- | ------------------- |
| `MemoryKindNote`    | note                |
| `MemoryKindQuote`   | quote               |
| `MemoryKindThought` | thought             |
| `MemoryKindSummary` | summary             |
| `MemoryKindTask`    | task                |