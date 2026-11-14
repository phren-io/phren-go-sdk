# ListProjectsResponse

A page of projects.


## Fields

| Field                                                      | Type                                                       | Required                                                   | Description                                                |
| ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- |
| `Projects`                                                 | [][components.Project](../../models/components/project.md) | :heavy_check_mark:                                         | The projects on this page.                                 |
| `NextPageToken`                                            | `*string`                                                  | :heavy_minus_sign:                                         | Token for the next page. Absent on the last page.          |