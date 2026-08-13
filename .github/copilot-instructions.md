## Copilot instructions for ONTAP automation documentation

### Repository overview
Product: ONTAP automation

This repository documents the automation options available for administering ONTAP storage systems. It focuses on the ONTAP REST API as the primary interface with a description of additional software tools and techniques as needed. There is also documentation with links supporting customer migration from ONTAPI (ZAPI) to the REST equivalents.

### Repository structure
- `get-started/` – Introduction to REST with the access prerequisites, first API call, and overview of automation options.
- `rest/` – Core REST behavior, request/response patterns, asynchronous job handling, input variables, and RBAC model details.
- `resources/` – Category-based summaries of the ONTAP REST resources such as storage, networking, NAS, SAN, security, and SVM.
- `workflows/` – Task-oriented REST workflow procedures using curl/JSON patterns across categories such as cluster, security, networking, storage, NAS, and SVM tasks.
- `migrate/` – Guidance for moving automation systems from *ONTAPI* and selected CLI usage patterns to the REST equivalents.
- `python/` – ONTAP Python client library (*netapp-ontap*) overview with sample usage content.
- `pstk/` – NetApp.ONTAP PowerShell Toolkit overview for ONTAP administration deployed on Windows hosts.
- `sw-tools/` – Original and supporting tooling context including the NetApp Manageability SDK and references.
- `reference/` – Assistance accessing and using the ONTAP API reference documentation.
- `additional/` – Supplemental links and related automation resources.
- `store-redirects/` – Redirect placeholder pages that preserve URLs and topic paths (no actual content).
- `media/` – Shared media assets referenced by the documentation pages.

### Product-specific context
**Architecture and components:**
- ONTAP REST automation is based on HTTP calls from the client to the ONTAP cluster or SVM using industry best practices.
- The ONTAP REST API is the strategic automation interface; ONTAPI (ZAPI) content is presented primarily for migration support.
- ONTAP can process REST operations synchronously or asynchronously; long-running operations return a *Job* resource that clients poll for the completion state.
- Authorization is role-based (*RBAC*) with access scoped at the cluster or SVM level; REST roles are mapped to traditional role behavior.

**Key concepts:**
- A *workflow* is a sequenced set of steps (REST calls and any related actions) needed to complete a single administrative goal.
- REST interactions follow an HTTP request/response transaction model based on the CRUD-style resource operations with JSON payloads.
- Object access is resource-oriented and commonly uses UUID for identification with property filters available to queried specific objects.
- A data *SVM* (storage virtual machine) is the primary SVM type exposed through REST for most tenant-level operations.

**Naming conventions and terminology:**
- *ONTAPI* and *ZAPI* can be used interchangeably for the proprietary API provided through the NetApp Manageability SDK; ONTAPI is the correct term.
- REST endpoint paths follow ONTAP resource naming with the prefix */api/...*.
- CLI passthrough operations use the */private/cli* base path.
- Workflow examples use uppercase Bash-style variable tokens such as *$FQDN_IP*, *$CLUSTER_ID*, and *$BASIC_AUTH*.
- The Python client package name is *netapp-ontap* and the PowerShell toolkit name/module is *NetApp.ONTAP*.

### Typical user workflows
**Initial REST connectivity check:** Gather cluster management *LIF* (*logical interface*) and credentials → Issue a GET call to */api/cluster* (often with *fields* filtering) → Review JSON response → Use endpoint access for subsequent tasks.

**General REST automation task execution:** Select a workflow topic → Set required workflow variables → Run ordered curl/JSON REST steps → If async, poll the returned *Job* object → Confirm task completion and output state.

**RBAC setup for API access:** Identify required ONTAP resource paths and actions → Define or select cluster/SVM-scoped role privileges → Assign or create user accounts to roles → Validate allowed API operations.

**Migration from ONTAPI to REST:** Inventory existing ONTAPI/CLI automation calls → Use ONTAPI-to-REST mapping references → Replace calls with REST resource operations (or CLI passthrough when needed) → Validate behavior in target workflows.
