# ListSpaceOperationsResponse

A page of a resource's operations, newest first.


## Fields

| Field                                                                    | Type                                                                     | Required                                                                 | Description                                                              |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| `Operations`                                                             | [][components.SpaceOperation](../../models/components/spaceoperation.md) | :heavy_check_mark:                                                       | The operations on this page.                                             |
| `NextPageToken`                                                          | `*string`                                                                | :heavy_minus_sign:                                                       | Token for the next page. Absent on the last page.                        |