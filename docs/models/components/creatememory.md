# CreateMemory

A piece of text an agent remembers. Creating one indexes it for the space's
queries in the background; its content can't be changed.


## Fields

| Field                                | Type                                 | Required                             | Description                          |
| ------------------------------------ | ------------------------------------ | ------------------------------------ | ------------------------------------ |
| `Content`                            | `string`                             | :heavy_check_mark:                   | Plain text, at most 32 KiB in UTF-8. |