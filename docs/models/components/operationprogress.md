# OperationProgress

How far an import has got, in the file's lines (RFC 008). A line the target
already holds is skipped, not an error. An export's `total` is the memories
it holds.


## Fields

| Field                                                               | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `Total`                                                             | `int`                                                               | :heavy_check_mark:                                                  | Lines to import, or memories exported.                              |
| `Imported`                                                          | `int`                                                               | :heavy_check_mark:                                                  | Lines written so far, whole or split into parts.                    |
| `Skipped`                                                           | `int`                                                               | :heavy_check_mark:                                                  | Lines skipped because the target already holds them.                |
| `Split`                                                             | `int`                                                               | :heavy_check_mark:                                                  | Lines over the 32 KiB memory limit, each written as numbered parts. |