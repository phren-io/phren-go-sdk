# OperationProgress

How far an export or import has got, in memories. A line of the file that
the target already holds (the same origin, or the same content) is skipped,
not an error.


## Fields

| Field                                                                                     | Type                                                                                      | Required                                                                                  | Description                                                                               |
| ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| `Total`                                                                                   | `int`                                                                                     | :heavy_check_mark:                                                                        | Memories in the file.                                                                     |
| `Done`                                                                                    | `int`                                                                                     | :heavy_check_mark:                                                                        | Memories written so far: exported, or created by the import.                              |
| `SkippedDuplicate`                                                                        | `int`                                                                                     | :heavy_check_mark:                                                                        | Lines skipped because the target already holds them.                                      |
| `Split`                                                                                   | `int`                                                                                     | :heavy_check_mark:                                                                        | Lines over the 32 KiB memory limit, each split into numbered parts that<br/>share its origin. |