# OrganizationsListRequest


## Fields

| Field                                           | Type                                            | Required                                        | Description                                     |
| ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- |
| `PageSize`                                      | `*int`                                          | :heavy_minus_sign:                              | Maximum number of results to return.            |
| `PageToken`                                     | `*string`                                       | :heavy_minus_sign:                              | Token from a previous response's nextPageToken. |
| `Filter`                                        | `*string`                                       | :heavy_minus_sign:                              | AIP-160 filter expression.                      |
| `ShowDeleted`                                   | `*bool`                                         | :heavy_minus_sign:                              | Include soft-deleted resources in the results.  |