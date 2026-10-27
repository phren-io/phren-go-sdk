# OrganizationInput

An organization: the top-level container that owns all other resources.


## Fields

| Field                                                                        | Type                                                                         | Required                                                                     | Description                                                                  | Example                                                                      |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `DisplayName`                                                                | `string`                                                                     | :heavy_check_mark:                                                           | Human-readable name: 1-63 characters, single line.                           | Acme Corp                                                                    |
| `State`                                                                      | [components.OrganizationState](../../models/components/organizationstate.md) | :heavy_check_mark:                                                           | Lifecycle state of an organization.                                          | active                                                                       |