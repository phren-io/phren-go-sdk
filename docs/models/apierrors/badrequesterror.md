# BadRequestError


## Fields

| Field                                                              | Type                                                               | Required                                                           | Description                                                        |
| ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ |
| `Type`                                                             | `*string`                                                          | :heavy_minus_sign:                                                 | URI identifying the problem type.                                  |
| `Title`                                                            | `string`                                                           | :heavy_check_mark:                                                 | Short, human-readable summary of the problem type.                 |
| `Status`                                                           | `int`                                                              | :heavy_check_mark:                                                 | HTTP status code.                                                  |
| `Detail`                                                           | `*string`                                                          | :heavy_minus_sign:                                                 | Human-readable explanation specific to this occurrence.            |
| `HTTPMeta`                                                         | [components.HTTPMetadata](../../models/components/httpmetadata.md) | :heavy_check_mark:                                                 | N/A                                                                |