# CreateTeamMember

An organization member's membership in a team. Organization admins manage
every team without being members.


## Fields

| Field                                                                                       | Type                                                                                        | Required                                                                                    | Description                                                                                 |
| ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| `Member`                                                                                    | `string`                                                                                    | :heavy_check_mark:                                                                          | The organization member added to the team:<br/>`organizations/{organization}/members/{member}`. |
| `Roles`                                                                                     | [][components.MemberRole](../../models/components/memberrole.md)                            | :heavy_minus_sign:                                                                          | Roles the member holds in the team. Empty for a plain member.                               |