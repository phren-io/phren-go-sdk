# ListTeamMembersResponse

A page of team members.


## Fields

| Field                                                            | Type                                                             | Required                                                         | Description                                                      |
| ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- |
| `Members`                                                        | [][components.TeamMember](../../models/components/teammember.md) | :heavy_check_mark:                                               | The members on this page.                                        |
| `NextPageToken`                                                  | `*string`                                                        | :heavy_minus_sign:                                               | Token for the next page. Absent on the last page.                |