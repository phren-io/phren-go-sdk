# ListOrganizationsResponse

A page of organizations.


## Fields

| Field                                                                | Type                                                                 | Required                                                             | Description                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `Self`                                                               | `string`                                                             | :heavy_check_mark:                                                   | URL of this page.                                                    |
| `First`                                                              | `string`                                                             | :heavy_check_mark:                                                   | URL of the first page.                                               |
| `Prev`                                                               | `*string`                                                            | :heavy_minus_sign:                                                   | URL of the previous page. Absent on the first page.                  |
| `Next`                                                               | `*string`                                                            | :heavy_minus_sign:                                                   | URL of the next page. Absent on the last page.                       |
| `Organizations`                                                      | [][components.Organization](../../models/components/organization.md) | :heavy_check_mark:                                                   | The organizations on this page.                                      |