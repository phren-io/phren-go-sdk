# ListOrganizationsResponse

A page of organizations.


## Fields

| Field                                                                | Type                                                                 | Required                                                             | Description                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `Organizations`                                                      | [][components.Organization](../../models/components/organization.md) | :heavy_check_mark:                                                   | The organizations on this page.                                      |
| `NextPageToken`                                                      | `*string`                                                            | :heavy_minus_sign:                                                   | Token for the next page. Absent on the last page.                    |