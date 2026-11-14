# Team

A team in an organization. Teams own projects, and through them spaces and
memories.


## Fields

| Field                                                       | Type                                                        | Required                                                    | Description                                                 |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| `Name`                                                      | `string`                                                    | :heavy_check_mark:                                          | Resource name: `organizations/{organization}/teams/{team}`. |
| `DisplayName`                                               | `string`                                                    | :heavy_check_mark:                                          | Human-readable name.                                        |
| `CreatedBy`                                                 | `string`                                                    | :heavy_check_mark:                                          | Name of the user that created the team.                     |
| `CreatedAt`                                                 | [time.Time](https://pkg.go.dev/time#Time)                   | :heavy_check_mark:                                          | When the team was created.                                  |