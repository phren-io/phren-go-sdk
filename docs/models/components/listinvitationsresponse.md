# ListInvitationsResponse

A page of invitations.


## Fields

| Field                                                            | Type                                                             | Required                                                         | Description                                                      |
| ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- |
| `Invitations`                                                    | [][components.Invitation](../../models/components/invitation.md) | :heavy_check_mark:                                               | The invitations on this page.                                    |
| `NextPageToken`                                                  | `*string`                                                        | :heavy_minus_sign:                                               | Token for the next page. Absent on the last page.                |