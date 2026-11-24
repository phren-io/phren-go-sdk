# QuerySpaceRequest

A question to search a space's memories with.


## Fields

| Field                                                            | Type                                                             | Required                                                         | Description                                                      |
| ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- |
| `Query`                                                          | `string`                                                         | :heavy_check_mark:                                               | The question, in natural language. At most 2 KiB in UTF-8.       |
| `PageSize`                                                       | `*int`                                                           | :heavy_minus_sign:                                               | The most results to return. Defaults to 10.                      |
| `Kinds`                                                          | [][components.MemoryKind](../../models/components/memorykind.md) | :heavy_minus_sign:                                               | Keeps memories of any of these kinds. All kinds when absent.     |
| `Labels`                                                         | []`string`                                                       | :heavy_minus_sign:                                               | Keeps memories that have every one of these labels.              |