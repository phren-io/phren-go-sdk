# CreateProjectMember

An organization member's membership in a project. Organization admins
manage every project without being members.


## Fields

| Field                                                                                          | Type                                                                                           | Required                                                                                       | Description                                                                                    |
| ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| `Member`                                                                                       | `string`                                                                                       | :heavy_check_mark:                                                                             | The organization member added to the project:<br/>`organizations/{organization}/members/{member}`. |
| `Roles`                                                                                        | [][components.MemberRole](../../models/components/memberrole.md)                               | :heavy_minus_sign:                                                                             | Roles the member holds in the project. Empty for a plain member.                               |