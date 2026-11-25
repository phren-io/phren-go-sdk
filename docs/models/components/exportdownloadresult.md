# ExportDownloadResult

How a download of an export ended.

## Example Usage

```go
import (
	"github.com/phren-io/phren-go-sdk/models/components"
)

value := components.ExportDownloadResultStarted

// Open enum: custom values can be created with a direct type cast
custom := components.ExportDownloadResult("custom_value")
```


## Values

| Name                           | Value                          |
| ------------------------------ | ------------------------------ |
| `ExportDownloadResultStarted`  | started                        |
| `ExportDownloadResultComplete` | complete                       |
| `ExportDownloadResultAborted`  | aborted                        |