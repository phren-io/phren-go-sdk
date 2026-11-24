# QuerySpaceResponse

The best matches, most relevant first, at most one per memory. Memories
become searchable shortly after they're created, and stop matching shortly
after they're deleted.


## Fields

| Field                                                              | Type                                                               | Required                                                           | Description                                                        |
| ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ |
| `Results`                                                          | [][components.QueryResult](../../models/components/queryresult.md) | :heavy_check_mark:                                                 | The matching memories.                                             |