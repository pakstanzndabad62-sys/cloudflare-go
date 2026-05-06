# Changelog

## 7.0.0 (2026-04-30)

Full Changelog: [v6.10.0...v7.0.0](https://github.com/cloudflare/cloudflare-go/compare/v6.10.0...v7.0.0)

This is a major version release that includes breaking changes to three packages: `ai_search`, `email_security`, and `workers`. These changes reflect upstream API specification updates that improve type correctness and consistency. Non-breaking features and updates are also included across several other packages.

## Please ensure you read through the list of changes below before moving to this version - this will help you understand any down or upstream issues it may cause to your environments.

---

## Breaking Changes

See the [v7.0.0 Migration Guide](./docs/migration-guides/v7.0.0-migration-guide.md) for before/after code examples and actions needed for each change.

### AI Search - SearchForAgents Metadata Removed

The `SearchForAgents` nested type has been removed from all instance metadata structs. This field is no longer part of the API specification.

**Removed Types:**
- `InstanceNewResponseMetadataSearchForAgents`
- `InstanceUpdateResponseMetadataSearchForAgents`
- `InstanceListResponseMetadataSearchForAgents`
- `InstanceDeleteResponseMetadataSearchForAgents`
- `InstanceReadResponseMetadataSearchForAgents`
- `InstanceNewParamsMetadataSearchForAgents`
- `InstanceUpdateParamsMetadataSearchForAgents`
- `NamespaceInstanceNewResponseMetadataSearchForAgents`
- `NamespaceInstanceUpdateResponseMetadataSearchForAgents`
- `NamespaceInstanceListResponseMetadataSearchForAgents`
- `NamespaceInstanceDeleteResponseMetadataSearchForAgents`
- `NamespaceInstanceReadResponseMetadataSearchForAgents`
- `NamespaceInstanceNewParamsMetadataSearchForAgents`
- `NamespaceInstanceUpdateParamsMetadataSearchForAgents`

### Email Security - Path Parameter Type Changes (`int64` to `string`)

Multiple Email Security settings sub-resources have changed their path parameter types from `int64` to `string`. This affects `Delete`, `Edit`, and `Get` methods across the following services:

- `AllowPolicies` (`policyID int64` -> `policyID string`)
- `BlockSenders` (`patternID int64` -> `patternID string`)
- `Domains` (`domainID int64` -> `domainID string`)
- `ImpersonationRegistry` (`displayNameID int64` -> `impersonationRegistryID string`)
- `TrustedDomains` (`trustedDomainID int64` -> `trustedDomainID string`)

### Email Security - Investigate Parameter Rename

The `Investigate.Get`, `Investigate.Move.New`, and `Investigate.Reclassify.New` methods now use `investigateID` instead of `postfixID` as the path parameter name.

### Email Security - Domains BulkDelete Method Removed

The `SettingDomainService.BulkDelete` method and its associated types have been removed:

- `SettingDomainBulkDeleteResponse`
- `SettingDomainBulkDeleteParams`

### Email Security - TrustedDomains Return Type Change

`SettingTrustedDomainService.New` now returns `*SettingTrustedDomainNewResponse` instead of `*SettingTrustedDomainNewResponseUnion`.

### Email Security - Investigate.Move Return Type Change

`InvestigateMoveService.New` now returns `*pagination.SinglePage[InvestigateMoveNewResponse]` instead of `*[]InvestigateMoveNewResponse`.

### Workers - Observability Telemetry Filter Restructuring

The observability telemetry filter parameter types have been restructured to support nested filter groups. New discriminated union types replace the previous flat filter arrays:

- `ObservabilityTelemetryKeysParams.Filters` now accepts `FiltersObjectFilterUnion` (was `[]interface{}`)
- `ObservabilityTelemetryQueryParams.Parameters.Filters` now accepts `FiltersObjectFilterUnion`
- `ObservabilityTelemetryValuesParams.Filters` now accepts `FiltersObjectFilterUnion`

New types include `FiltersObjectFiltersObject` (for group filters with `FilterCombination`) and `FiltersWorkersObservabilityFilterLeaf` (for leaf filters with typed `Operation`, `Type`, and `Value` fields).

---

## Features

### Organizations (`client.Organizations`)

- **NEW SERVICE**: `client.Organizations.Logs.Audit` -- query organization audit logs
  - `List()` - Retrieve audit logs with cursor-based pagination

### Browser Rendering (`client.BrowserRendering`)

- `client.BrowserRendering.Devtools.Browser.Targets.Close()` -- close a specific browser target (tab, page) by ID

### Queues (`client.Queues`)

- `client.Queues.GetMetrics()` -- retrieve queue metrics for a specific queue

### AI Search (`client.AISearch`)

- Added `WaitForCompletion` parameter to `NamespaceInstanceItemNewOrUpdateParams` and `NamespaceInstanceItemSyncParams` for synchronous indexing confirmation

---

## Bug Fixes

- **Magic Transit**: `ConnectorService.List` parameter name corrected from `query` to `params` (non-functional, affects generated documentation only)

---

## Deprecations

None in this release.
