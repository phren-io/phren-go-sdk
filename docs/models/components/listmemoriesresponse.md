# ListMemoriesResponse

A page of memories, newest first.


## Fields

| Field                                                    | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `Memories`                                               | [][components.Memory](../../models/components/memory.md) | :heavy_check_mark:                                       | The memories on this page.                               |
| `NextPageToken`                                          | `*string`                                                | :heavy_minus_sign:                                       | Token for the next page. Absent on the last page.        |