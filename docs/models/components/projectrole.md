# ProjectRole

A member's role in a project. Each includes the next: admins manage the
project's members and spaces, editors also write and delete memories in
its spaces, and viewers read and search them.

## Example Usage

```go
import (
	"github.com/phren-io/phren-go-sdk/models/components"
)

value := components.ProjectRoleAdmin

// Open enum: custom values can be created with a direct type cast
custom := components.ProjectRole("custom_value")
```


## Values

| Name                | Value               |
| ------------------- | ------------------- |
| `ProjectRoleAdmin`  | admin               |
| `ProjectRoleEditor` | editor              |
| `ProjectRoleViewer` | viewer              |