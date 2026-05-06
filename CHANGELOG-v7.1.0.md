## 7.1.0 (2026-05-04)

Full Changelog: [v7.0.0...v7.1.0](https://github.com/cloudflare/cloudflare-go/compare/v7.0.0...v7.1.0)

---

## Features

### Security Center - New Insights Sub-Resources (client.SecurityCenter.Insights)

Three new sub-services added under `client.SecurityCenter.Insights`:

**AuditLogs** (`client.SecurityCenter.Insights.AuditLogs`)

- `List(ctx, params) -> *pagination.CursorPagination[InsightAuditLogListResponse]`
- `ListByInsight(ctx, issueID, params) -> *pagination.CursorPagination[InsightAuditLogListByInsightResponse]`

New response types: `InsightAuditLogListResponse`, `InsightAuditLogListByInsightResponse`

**Classification** (`client.SecurityCenter.Insights.Classification`)

- `Update(ctx, issueID, params) -> *InsightClassificationUpdateResponse`

New response types: `InsightClassificationUpdateResponse`

**Context** (`client.SecurityCenter.Insights.Context`)

- `Get(ctx, issueID, query) -> *InsightContextGetResponse`

New response types: `InsightContextGetResponse`

### Zero Trust - Device Deployment Groups (client.ZeroTrust.Devices.DeploymentGroups)

New service `client.ZeroTrust.Devices.DeploymentGroups`:

- `New(ctx, params) -> *DeploymentGroup`
- `List(ctx, params) -> *pagination.V4PagePaginationArray[DeploymentGroup]`
- `Delete(ctx, groupID, body) -> *DeviceDeploymentGroupDeleteResponse`
- `Edit(ctx, groupID, params) -> *DeploymentGroup`
- `Get(ctx, groupID, query) -> *DeploymentGroup`

New response types: `DeploymentGroup`, `DeviceDeploymentGroupDeleteResponse`

### Queues - Metrics Endpoint (client.Queues)

New method on `client.Queues`:

- `GetMetrics(ctx, queueID, query) -> *QueueGetMetricsResponse`

New response types: `QueueGetMetricsResponse`

### Organizations - Audit Logs (client.Organizations.Logs.Audit)

New service `client.Organizations.Logs.Audit`:

- `List(ctx, organizationID, query) -> *pagination.CursorPaginationAfter[LogAuditListResponse]`

New response types: `LogAuditListResponse`

---

## Deprecations

None.

## Bug Fixes

None.
