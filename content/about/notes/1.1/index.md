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

- **Allow All Outbound Traffic**. Allow all outbound traffic by default now.   To enforce no outbound traffic at mesh wide, configure ```global.outboundTrafficPolicy.mode``` to ```REGISTRY_ONLY```

- **Egress Gateway Disabled By Default**.- Egress gateway is disabled by default now.  To enable it, configure gateways.istio-egressgateway.enabled to ```true```

- **Simpler Service Entry Resources**. Reduced the need to bind virtual services to service entry resources greatly simplifying the resources.

- TBD: note about sidecar and export_to API.

## Security

- **Readines and Liveness Probes**. Istio now supports Kubernetes' HTTP readiness and liveness probes when mutual TLS is enabled.
TBD: LINK TO DOC

- **Cluster RBAC Configuration**.  Replaced the `RbacConfig` resource with the `ClusterRbacConfig` resource to implement the correct cluster scope.
Refer to our guide on [Migrating the `RbacConfig` to `ClusterRbacConfig`](/docs/setup/kubernetes/upgrading-istio#migrating-the-rbacconfig-to-clusterrbacconfig)
for migration instructions.

## Multiclusters

- **Non-Routable L3 Networks**. A single Istio control plane can now be used in multicluster environments with non-routable
L3 networks.
TBD: LINK

- **Multiple Control Planes**. Multiple Istio control plane multicluster is now supported.
TBD: LINK

## Policies and telemetry

- **Policy Checks Off By Default**. Policy checks are now turned off by default which improves performance for most customer scenarios.
TBD: LINK

- **Kiali**. [Kiali](https://www.kiali.io) replaces the [Service Graph addon](https://github.com/istio/istio/issues/9066) and provides
a richer visualization experience. See the [Kiali Task](/docs/tasks/telemetry/kiali/) for more details.

- **Reduced Overhead**. There have been several performance and scale improvements including:

    - Significant reduction in default collection of Envoy-generated statistics (configurable via annotations)

    - Added load-shedding functionality to Mixer workloads.

    - Improved the protocol between Envoy and Mixer.

- **Control Headers and Routing**. It's now possible to create adapters that can be used to influence
an incoming request's headers and routing. TBD: LINK

- **Out of Process Adapters**. The out-of-process adapter functionality is now ready for production
use. TBD: LINK
 
- **Tracing Improvements**. There have been many improvements in our overall tracing story:

    - We now use 128 bit trace ids
    - There are some enhanced deployment options for Jaeger and Zipkin TBD: LINKS
    - We now support sending trace data to LightStep
    - Enabled full disablement of tracing for Mixer-backed services TBD: REPHRASE
    - Added policy decision-aware tracing. TBD: LINK

- **Default TCP Metrics**. There are now default metrics for tracking TCP connections.

## Configuration management

- **Galley**. Galley is now used as the primary config ingestion and distribution mechanism within Istio. It provides
a robust model to validate, transform, and distribute configuration state to Istio components, insulating the components
from Kubernetes details. Galley uses the [Mesh Configuration Protocol (MCP)](https://github.com/istio/api/tree/{{< source_branch_name >}}/mcp) to interact with components. TBD: LINK TO MCP

- **Monitoring Port**. Galley's default monitoring port was changed from 9093 to 15014.

## `istioctl` and `kubectl`

- **Validate Command**. Added the [`istioctl validate`](/docs/reference/commands/istioctl/#istioctl-validate) command for offline validation of Istio Kubernetes resources. This replaces

- **Verify-Install Command**. Added the [`istioctl experimental verify-install`](/docs/reference/commands/istioctl/#istioctl-experimental-verify-install) command used to verify the status of an 
Istio installation given a specified installation YAML file.

- **Deprecated Commands**. Deprecated the `istioctl create`, `istioctl replace`, `istioctl get`, and `istioctl delete` commands. Use the [`kubectl`](https://kubernetes.io/docs/tasks/tools/install-kubectl) equivalents instead.
The `istioctl gen-deploy` command is also being deprecated. Use a [`helm template`](/docs/setup/kubernetes/install/helm/#option-1-install-with-helm-via-helm-template) instead.
This command will be removed completely in the 1.2 release.

- **Short Commands**. 'kubectl' now includes short commands for gateways, virtual services, destination rules and service entries.
