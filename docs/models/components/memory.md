# Memory

A piece of text an agent remembers. Creating one indexes it for the space's
queries in the background; its content can't be changed.


## Fields

| Field                                                                           | Type                                                                            | Required                                                                        | Description                                                                     |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| `Name`                                                                          | `string`                                                                        | :heavy_check_mark:                                                              | Resource name: `organizations/{organization}/spaces/{space}/memories/{memory}`. |
| `Content`                                                                       | `string`                                                                        | :heavy_check_mark:                                                              | Plain text, at most 32 KiB in UTF-8.                                            |
| `CreatedBy`                                                                     | `string`                                                                        | :heavy_check_mark:                                                              | Name of the user that created the memory.                                       |
| `CreatedAt`                                                                     | [time.Time](https://pkg.go.dev/time#Time)                                       | :heavy_check_mark:                                                              | When the memory was created.                                                    |