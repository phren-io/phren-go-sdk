# ListLinkGrantsResponse

A page of link grants.


## Fields

| Field                                                          | Type                                                           | Required                                                       | Description                                                    |
| -------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------- |
| `LinkGrants`                                                   | [][components.LinkGrant](../../models/components/linkgrant.md) | :heavy_check_mark:                                             | The grants on this page.                                       |
| `NextPageToken`                                                | `*string`                                                      | :heavy_minus_sign:                                             | Token for the next page. Absent on the last page.              |