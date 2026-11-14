# MemoriesListRequest


## Fields

| Field                                           | Type                                            | Required                                        | Description                                     | Example                                         |
| ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- |
| `PageSize`                                      | `*int`                                          | :heavy_minus_sign:                              | Maximum number of results to return.            | 50                                              |
| `PageToken`                                     | `*string`                                       | :heavy_minus_sign:                              | Token from a previous response's nextPageToken. |                                                 |
| `Filter`                                        | `*string`                                       | :heavy_minus_sign:                              | AIP-160 filter expression.                      |                                                 |
| `Organization`                                  | `string`                                        | :heavy_check_mark:                              | N/A                                             | acme                                            |
| `Space`                                         | `string`                                        | :heavy_check_mark:                              | N/A                                             | notes                                           |