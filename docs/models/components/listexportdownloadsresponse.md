# ListExportDownloadsResponse

A page of an export's downloads, newest first.


## Fields

| Field                                                                    | Type                                                                     | Required                                                                 | Description                                                              |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| `Downloads`                                                              | [][components.ExportDownload](../../models/components/exportdownload.md) | :heavy_check_mark:                                                       | The downloads on this page.                                              |
| `NextPageToken`                                                          | `*string`                                                                | :heavy_minus_sign:                                                       | Token for the next page. Absent on the last page.                        |