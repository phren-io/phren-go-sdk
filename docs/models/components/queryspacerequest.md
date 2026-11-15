# QuerySpaceRequest

A question to search a space's memories with.


## Fields

| Field                                                      | Type                                                       | Required                                                   | Description                                                |
| ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- |
| `Query`                                                    | `string`                                                   | :heavy_check_mark:                                         | The question, in natural language. At most 2 KiB in UTF-8. |
| `PageSize`                                                 | `*int`                                                     | :heavy_minus_sign:                                         | The most results to return. Defaults to 10.                |