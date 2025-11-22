# BTP Service Manager Skill - Progress Tracking

**Skill Name**: btp-service-manager
**Source Documentation**: https://github.com/SAP-docs/btp-service-manager/tree/main/docs
**Last Updated**: 2025-11-22
**Status**: Complete

---

## Documentation Sources Analyzed

### Main Index
- [x] `docs/index.md` - Main documentation structure and navigation

### Service Consumption Overview
- [x] `docs/Service-Consumption/consuming-services-in-sap-btp-f13b6c6.md` - Service creation and binding fundamentals

---

## SAP Service Manager Core (docs/Service-Consumption/SAP-Service-Manager/)

### Overview & Concepts
- [x] `sap-service-manager-3a27b85.md` - Core overview (platforms, brokers, instances, bindings, plans, offerings)
- [x] `sap-service-manager-api-groups-9b97aee.md` - API groups (Platforms, Instances, Bindings, Plans, Offerings, Operations)
- [x] `sap-service-manager-broker-plans-917a8a7.md` - Broker plans (subaccount-admin, subaccount-audit, container)
- [x] `sap-service-manager-roles-d95fbe7.md` - Roles (Subaccount Service Administrator, Subaccount Service Viewer)

### Setup & Authentication
- [x] `installing-the-service-manager-control-smctl-command-line-tool-93532bd.md` - SMCTL installation
- [x] `logging-in-to-sap-service-manager-22dea57.md` - Login procedures with 2FA
- [x] `accessing-the-apis-93711c1.md` - API access (User tokens vs Client tokens)
- [x] `retrieve-an-oauth2-access-token-b6822e6.md` - OAuth2 token retrieval
- [x] `create-a-sap-service-manager-instance-and-binding-1ca5bbe.md` - Instance/binding setup with X.509
- [x] `assign-the-subaccount-service-administrator-collection-0735965.md` - Role assignment

### Rate Limiting & Filtering
- [x] `rate-limiting-97be679.md` - Three-tier rate limits (API-wide, resource-specific, method-specific)
- [x] `filtering-parameters-and-operators-3331c6e.md` - fieldQuery, labelQuery, operators (eq, ne, gt, lt, in, contains, etc.)

### Managing via Cockpit
- [x] `managing-services-using-the-sap-btp-cockpit-cdce096.md` - Cockpit overview

### Service Instances
- [x] `creating-service-instances-fad874a.md` - Overview of instance creation
- [x] `creating-service-instances-in-cloud-foundry-6d6846d.md` - CF instance creation (wizard, naming rules)
- [x] `creating-service-instances-in-the-kyma-environment-422b446.md` - Kyma instances (links to external docs)
- [x] `creating-service-instances-in-the-kubernetes-environment-26227a9.md` - K8s instances with labels
- [x] `creating-instances-in-other-environments-bf71f6a.md` - "Other" environment instances
- [x] `creating-user-provided-service-instances-in-cloud-foundry-environment-7c0125b.md` - User-provided services
- [x] `deleting-service-instances-753463e.md` - Deletion procedures and prerequisites

### Service Bindings
- [x] `service-bindings-392eb36.md` - Bindings API overview (list, create, get, delete)
- [x] `binding-service-instances-to-cloud-foundry-applications-0e6850d.md` - CF app binding
- [x] `creating-service-bindings-in-kubernetes-5c7aa31.md` - K8s bindings (links to external)
- [x] `creating-service-bindings-in-kyma-9467024.md` - Kyma bindings (links to external)
- [x] `creating-service-keys-in-cloud-foundry-6fcac08.md` - Service keys for external access

### SMCTL CLI Commands
- [x] `login-a8ed7cf.md` - `smctl login` (password/client-credentials, X.509 support)
- [x] `logout-54f7e42.md` - `smctl logout`
- [x] `provision-b327b66.md` - `smctl provision` (sync/async modes)
- [x] `bind-f53ff26.md` - `smctl bind` (sync/async modes)
- [x] `deprovision-f48502c.md` - `smctl deprovision` (force flag, sync/async)
- [x] `marketplace-ae6874a.md` - `smctl marketplace` (list offerings/plans)
- [x] `register-broker-3e7a312.md` - `smctl register-broker`
- [x] `register-platform-4fe2d10.md` - `smctl register-platform`
- [x] `list-instances-728f1b6.md` - `smctl list-instances`
- [x] `list-bindings-0078d1a.md` - `smctl list-bindings`
- [x] `get-operation-status-3b330bb.md` - Operation status API

### BTP CLI Commands
- [x] `create-services-instance-5a44ad8.md` - `btp create services/instance`
- [x] `create-services-binding-7cf9dc5.md` - `btp create services/binding`
- [x] `get-services-instance-adb4c54.md` - `btp get services/instance`
- [x] `platforms-7610c08.md` - `btp` platform commands (list, get, register, update, unregister)
- [x] `brokers-743f3f7.md` - Broker operations (register, update, list, delete)
- [x] `offerings-5708056.md` - Offerings operations (list-offerings, list-plans, marketplace)
- [x] `instances-23af00d.md` - Instance operations (provision, get, list, deprovision)

---

## Consuming SAP BTP Services from Various Environments

### Overview
- [x] `consuming-sap-btp-services-from-various-aa2ba14.md` - Multi-environment overview (CF, Neo, Kyma, K8s)

### Kubernetes Consumption
- [x] `consuming-sap-btp-services-in-kubernetes-b5a35bf.md` - K8s consumption overview
- [x] `prerequisites-dd5faaa.md` - Prerequisites (kubectl 1.7+, SMCTL v1.10.1, Helm v3.1.2)
- [x] `setup-e977f23.md` - Setup (cert-manager, service-operator-access plan, Helm deploy)
- [x] `working-with-sap-btp-service-operator-0ccebd7.md` - ServiceInstance/ServiceBinding CRDs with YAML examples

### Migration
- [x] `migrating-from-svcat-to-sap-btp-service-ec7f5c7.md` - Migration from Service Catalog (scan, validate, migrate phases)

---

## Information Extracted & Covered in Skill

### SKILL.md (Core Content)
1. **Overview & Architecture**
   - SAP Service Manager as central registry
   - Six primary resources: Platforms, Brokers, Instances, Bindings, Plans, Offerings
   - Open Service Broker API (OSBAPI) support

2. **Authentication & Authorization**
   - Three broker plans with scopes
   - Two roles with permissions
   - OAuth2 (password and client-credentials flows)
   - X.509 certificate support

3. **Quick Start**
   - SMCTL installation
   - Login procedure with 2FA
   - Instance provisioning
   - Binding creation

4. **CLI Commands**
   - Complete SMCTL command reference
   - BTP CLI command reference
   - All parameters and flags documented

5. **API Reference**
   - Rate limiting (3 tiers)
   - Filtering operators
   - API groups overview

6. **Environment-Specific Guides**
   - Cloud Foundry
   - Kyma
   - Kubernetes (with YAML)
   - Other environments

### references/ (Progressive Disclosure)
1. **api-reference.md** - Complete API endpoints, parameters, responses
2. **smctl-commands.md** - Full SMCTL CLI reference
3. **btp-cli-commands.md** - Full BTP CLI reference
4. **kubernetes-operator.md** - ServiceInstance/ServiceBinding CRDs, setup, migration
5. **rate-limiting-filtering.md** - Detailed rate limits and filter operators
6. **roles-permissions.md** - Complete roles, plans, and scopes

### templates/
1. **service-instance-cf.json** - Cloud Foundry instance parameters
2. **service-binding-cf.json** - Cloud Foundry binding parameters
3. **service-instance-k8s.yaml** - Kubernetes ServiceInstance CRD
4. **service-binding-k8s.yaml** - Kubernetes ServiceBinding CRD
5. **oauth-token-request.sh** - OAuth2 token retrieval script

---

## Documentation Links for Updates

### Primary Sources
- **GitHub Docs**: https://github.com/SAP-docs/btp-service-manager/tree/main/docs
- **SAP Help Portal**: https://help.sap.com/docs/service-manager
- **SAP BTP Service Operator**: https://github.com/SAP/sap-btp-service-operator
- **SMCTL Releases**: https://github.com/Peripli/service-manager-cli/releases

### API Documentation
- **Swagger UI**: `https://service-manager.cfapps.<region>.hana.ondemand.com/swaggerui/swagger-ui.html`
- **Regions**: https://help.sap.com/docs/btp/sap-business-technology-platform/regions-and-api-endpoints-available-for-cloud-foundry-environment

### Related Documentation
- **BTP Cockpit**: https://cockpit.btp.cloud.sap/
- **Cloud Foundry CLI**: https://docs.cloudfoundry.org/cf-cli/
- **Kyma Services**: https://help.sap.com/docs/btp/sap-business-technology-platform/using-services-in-kyma-environment
- **cert-manager**: https://cert-manager.io/docs/installation/kubernetes/

---

## Verification Checklist

- [x] All index.md files analyzed
- [x] All SAP-Service-Manager/*.md files analyzed
- [x] All Consuming-SAP-BTP-Services-from-Various-Environments/*.md files analyzed
- [x] SMCTL commands documented with all parameters
- [x] BTP CLI commands documented with all parameters
- [x] API endpoints documented
- [x] Kubernetes YAML examples included
- [x] Rate limits documented
- [x] Filtering operators documented
- [x] Roles and permissions documented
- [x] Authentication flows documented
- [x] Documentation links included for updates

---

## Notes

1. Several Kyma/K8s documentation pages redirect to external SAP Help Portal
2. SMCTL is the dedicated CLI; BTP CLI also supports service management
3. Service operator GitHub repo has additional technical details
4. Rate limiting is three-tiered and operates concurrently
5. X.509 certificates supported for enhanced security

---

**Skill Status**: Ready for Production
**Completeness**: 100% of available documentation extracted
**Last Verification**: 2025-11-22
