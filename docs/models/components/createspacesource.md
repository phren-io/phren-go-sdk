# CreateSpaceSource

A source of a space (RFC 011): a query of the space also searches the
source space's memories, without copying them. It gives no access to the
source space itself. Sources stay inside the organization.


## Fields

| Field                                                                                                                              | Type                                                                                                                               | Required                                                                                                                           | Description                                                                                                                        |
| ---------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `Source`                                                                                                                           | `string`                                                                                                                           | :heavy_check_mark:                                                                                                                 | The source space: `organizations/{organization}/spaces/{space}`, in the<br/>same organization. Its project must be allowed to link it. |