# Project

A project in a team. Its spaces hold memories.


## Fields

| Field                                                                          | Type                                                                           | Required                                                                       | Description                                                                    |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ |
| `Name`                                                                         | `string`                                                                       | :heavy_check_mark:                                                             | Resource name: `organizations/{organization}/teams/{team}/projects/{project}`. |
| `DisplayName`                                                                  | `string`                                                                       | :heavy_check_mark:                                                             | Human-readable name.                                                           |
| `CreatedBy`                                                                    | `string`                                                                       | :heavy_check_mark:                                                             | Name of the user that created the project.                                     |
| `CreatedAt`                                                                    | [time.Time](https://pkg.go.dev/time#Time)                                      | :heavy_check_mark:                                                             | When the project was created.                                                  |