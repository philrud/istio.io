---
title: Istio 1.1
publishdate: 2019-03-12
icon: notes
---

We're proud to release Istio 1.1! It's been a while since 1.0 and we've done some significant improvements to make
the overall product more reliable, more efficient, and more scalable.

These release notes describe what's different between Istio 1.0 and Istio 1.1.

{{< relnote_links >}}

## Upgrades

- **Helm Changes**. 
TBD: need full content & links

- **TBD: TITLE**, Control plane and data plane requested resource changes
TBD: need full content & links

## Traffic management

- **Allow All Outbound Traffic**. Allow all outbound traffic by default now. 
To enforce no outbound traffic at mesh wide, configure `global.outboundTrafficPolicy.mode` to `REGISTRY_ONLY`
TBD: presumbly in Helm?

- **Egress Gateway Disabled By Default**.- Egress gateway is disabled by default now.
To enable it, configure `gateways.istio-egressgateway.enabled` to `true`
TBD: presumbly in Helm?

- **Simpler Service Entry Resources**. Reduced the need to bind virtual services to service entry resources greatly simplifying the resources.

- **Istio Ingress Deprecated**. Previously deprecated Istio ingress has been removed. Refer to [Securing Kubernetes Ingress with Cert-Manager](/docs/examples/advanced-gateways/ingress-certmgr/) example for more details on how to use Kubernetes Ingress resources with [gateways](/docs/concepts/traffic-management/#gateways).

- TBD: note about sidecar and export_to API.

## Security

- **Readines and Liveness Probes**. Added support of Kubernetes' HTTP readiness and liveness probes when mutual TLS is enabled.
TBD: LINK TO DOC

- **Cluster RBAC Configuration**.  Replaced the `RbacConfig` resource with the `ClusterRbacConfig` resource to implement the correct cluster scope.
See [Migrating the `RbacConfig` to `ClusterRbacConfig`](/docs/setup/kubernetes/upgrading-istio#migrating-the-rbacconfig-to-clusterrbacconfig)
for migration instructions.

- **Identity Provisioning Through SDS**. Provides stronger security with on-node key generation and dynamic certificate rotation without restarting Envoy.
See [Provisioning Identity through SDS](/docs/tasks/security/auth-sds) for more information.

- **Authorization for TCP Services**. Supports authorization for TCP services in addition to HTTP and gRPC services. 
See [Authorization for TCP Services](/docs/tasks/security/authz-tcp) for more information.

- **Authorization for End-User Groups**. Allows authorization based on `groups` claim or any list-typed claims in JWT.
See [Authorization for groups and list claims](/docs/tasks/security/rbac-groups/) for more information.

- **End-User Authentication with Per-Path Requirements**. Allows you to enable or disable JWT authentication based on the request path.
See [End-user authentication with per-path requirements](/docs/tasks/security/authn-policy/#end-user-authentication-with-per-path-requirements) for 
more information.

- **External Certificate Management on Ingress Gateway Controller**. Dynamically loads and rotates external certificates.

- **Vault PKI Integration**. Provides stronger security with Vault-protected signing keys and facilitates integration with existing Vault PKIs.
See [Istio Vault CA Integration](/docs/tasks/security/vault-ca) for more information.

- **Customized (non `cluster.local`) Trust Domains**. Supports organization- or cluster-specific trust domains in the identities.

## Multiclusters

- **Non-Routable L3 Networks**. Enabled using a single Istio control plane in multicluster environments with non-routable
L3 networks.
TBD: LINK

- **Multiple Control Planes**. Added support of multiple Istio control planes for multicluster environments.
TBD: LINK

## Policies and telemetry

- **Policy Checks Off By Default**. Changed policy checks to be turned off by default which improves performance for most customer scenarios.
TBD: LINK

- **Kiali**. Replaced the Service Graph addon](https://github.com/istio/istio/issues/9066) with [Kiali](https://www.kiali.io) to provide
a richer visualization experience. See the [Kiali Task](/docs/tasks/telemetry/kiali/) for more details.

- **Reduced Overhead**. Added several performance and scale improvements including:

    - Significant reduction in default collection of Envoy-generated statistics (configurable via annotations)

    - Added load-shedding functionality to Mixer workloads.

    - Improved the protocol between Envoy and Mixer.

- **Control Headers and Routing**. Added the option to create adapters to influence
an incoming request's headers and routing. TBD: LINK

- **Out of Process Adapters**. The out-of-process adapter functionality is now ready for production
TBD: LINK
 
- **Tracing Improvements**. There have been many improvements in our overall tracing story:

    -  You can now use 128 bit trace IDs.

    -  Added some enhanced deployment options for [Jaeger](https://istio.io/docs/tasks/telemetry/distributed-tracing/jaeger/)
    and [Zipkin](https://istio.io/docs/tasks/telemetry/distributed-tracing/zipkin/). TBD: are these right links for "deployment options"?

    - Added support of sending trace data to [LightStep](https://preliminary.istio.io/docs/tasks/telemetry/distributed-tracing/lightstep/)

    - Added the option to disable tracing for Mixer-backed services entirely. TBD: ADD LINK

    - Added policy decision-aware tracing. TBD: LINK

- **Default TCP Metrics**. Added default metrics for tracking TCP connections.

## Configuration management

- **Galley**. Added [Galley](https://istio.io/docs/concepts/what-is-istio/#galley) as the primary configuration ingestion and distribution mechanism within Istio. It provides
a robust model to validate, transform, and distribute configuration state to Istio components insulating the Istio components
from Kubernetes details. Galley uses the [Mesh Configuration Protocol (MCP)](https://github.com/istio/api/tree/{{< source_branch_name >}}/mcp) to interact with components. TBD: LINK TO MCP

- **Monitoring Port**. Changed Galley's default monitoring port from 9093 to 15014.

## `istioctl` and `kubectl`

- **Validate Command**. Added the [`istioctl validate`](/docs/reference/commands/istioctl/#istioctl-validate)
command for offline validation of Istio Kubernetes resources.

- **Verify-Install Command**. Added the [`istioctl experimental verify-install`](/docs/reference/commands/istioctl/#istioctl-experimental-verify-install) command to verify the status of an 
Istio installation given a specified installation YAML file.

- **Deprecated Commands**. Deprecated the `istioctl create`, `istioctl replace`, `istioctl get`, and `istioctl delete` commands. Use the [`kubectl`](https://kubernetes.io/docs/tasks/tools/install-kubectl) equivalents instead.
Deprecated the `istioctl gen-deploy` command too. Use a [`helm template`](/docs/setup/kubernetes/install/helm/#option-1-install-with-helm-via-helm-template) instead.
These commands will be removed in the 1.2 release.

- **Short Commands**. Included short commands in 'kubectl' for gateways, virtual services, destination rules and service entries. TBD: ADD LINK
