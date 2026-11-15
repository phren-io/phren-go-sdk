# Project

A project in an organization. Its members use its spaces, which hold
memories.


## Fields

| Field                                                             | Type                                                              | Required                                                          | Description                                                       |
| ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- |
| `Name`                                                            | `string`                                                          | :heavy_check_mark:                                                | Resource name: `organizations/{organization}/projects/{project}`. |
| `DisplayName`                                                     | `string`                                                          | :heavy_check_mark:                                                | Human-readable name.                                              |
| `CreatedBy`                                                       | `string`                                                          | :heavy_check_mark:                                                | Name of the user that created the project.                        |
| `CreatedAt`                                                       | [time.Time](https://pkg.go.dev/time#Time)                         | :heavy_check_mark:                                                | When the project was created.                                     |