# ListTeamsResponse

A page of teams.


## Fields

| Field                                                | Type                                                 | Required                                             | Description                                          |
| ---------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------- |
| `Teams`                                              | [][components.Team](../../models/components/team.md) | :heavy_check_mark:                                   | The teams on this page.                              |
| `NextPageToken`                                      | `*string`                                            | :heavy_minus_sign:                                   | Token for the next page. Absent on the last page.    |