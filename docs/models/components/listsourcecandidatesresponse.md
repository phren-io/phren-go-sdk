# ListSourceCandidatesResponse

A page of the spaces that can be added as sources.


## Fields

| Field                                                  | Type                                                   | Required                                               | Description                                            |
| ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ |
| `Spaces`                                               | [][components.Space](../../models/components/space.md) | :heavy_check_mark:                                     | The spaces on this page.                               |
| `NextPageToken`                                        | `*string`                                              | :heavy_minus_sign:                                     | Token for the next page. Absent on the last page.      |