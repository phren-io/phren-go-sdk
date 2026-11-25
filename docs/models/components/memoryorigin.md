# MemoryOrigin

An imported memory's original identity. The importer can't change it: it
comes from the exported file, and `createdBy` and `createdAt` on the memory
itself stay the import's.


## Fields

| Field                                                     | Type                                                      | Required                                                  | Description                                               |
| --------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------- |
| `Name`                                                    | `string`                                                  | :heavy_check_mark:                                        | The memory's resource name where it was created.          |
| `CreatedBy`                                               | `string`                                                  | :heavy_check_mark:                                        | Who created it there.                                     |
| `CreatedWith`                                             | `*string`                                                 | :heavy_minus_sign:                                        | The agent or API key that created it there, if any.       |
| `CreatedAt`                                               | [time.Time](https://pkg.go.dev/time#Time)                 | :heavy_check_mark:                                        | When it was created there.                                |
| `Part`                                                    | `*int`                                                    | :heavy_minus_sign:                                        | For a memory split on import: which part this is, from 1. |
| `Parts`                                                   | `*int`                                                    | :heavy_minus_sign:                                        | For a memory split on import: how many parts there are.   |