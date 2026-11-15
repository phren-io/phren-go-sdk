# QueryResult

A memory that matches a query.


## Fields

| Field                                                         | Type                                                          | Required                                                      | Description                                                   |
| ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- |
| `Memory`                                                      | `string`                                                      | :heavy_check_mark:                                            | Resource name of the memory.                                  |
| `Content`                                                     | `string`                                                      | :heavy_check_mark:                                            | The part of the memory that matched.                          |
| `Score`                                                       | `float64`                                                     | :heavy_check_mark:                                            | Relevance to the query, from 0 to 1. Higher is more relevant. |