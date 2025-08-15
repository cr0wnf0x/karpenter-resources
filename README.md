# Karpenter Resources Helm Chart

This Helm chart deploys Karpenter `GCENodeClass` and `NodePool` resources to a Kubernetes cluster.

## Chart Details

| Name | Version | Description |
|---|---|---|
| `karpenter-resources` | `0.1.0` | A Helm chart for deploying Karpenter GCENodeClass and NodePool resources |

## Prerequisites

*   Helm v3.0.0+
*   Karpenter installed on the cluster.

## Configuration

The following table lists the configurable parameters of the `karpenter-resources` chart and their default values.

| Parameter | Description | Default |
|---|---|---|
| `global.clusterName` | The name of the Kubernetes cluster. | `"default-cluster"` |
| `global.projectId` | The GCP project ID where the cluster is located. | `"default-project"` |
| `global.region` | The GCP region where the cluster is located. | `"default-region"` |
| `global.serviceAccount` | The service account to be used by Karpenter. | `"karpenter-system@{{ $.Values.global.projectId }}.iam.gserviceaccount.com"` |
| `nodePools` | A list of NodePools to create. | `[]` |

### NodePool Configuration

Each item in the `nodePools` list can have the following parameters:

| Parameter | Description |
|---|---|
| `name` | The name of the NodePool and the corresponding GCENodeClass. |
| `annotations` | Annotations to add to the NodePool. |
| `disruption` | Disruption settings for the NodePool. |
| `template.metadata.labels` | Labels to add to the nodes in the NodePool. |
| `template.spec.terminationGracePeriod` | The termination grace period for the nodes. |
| `template.spec.taints` | Taints to apply to the nodes. |
| `template.spec.requirements` | Node requirements for the NodePool. |
| `nodeClass.imageSelectorTerms` | Image selector terms for the GCENodeClass. |
| `nodeClass.networkTags` | Network tags for the GCENodeClass. |
| `nodeClass.disks` | Disk configuration for the GCENodeClass. |
| `nodeClass.kubeletConfiguration` | Kubelet configuration for the GCENodeClass. |
| `nodeClass.tags` | Tags for the GCENodeClass. |

## Usage

To install the chart with the release name `my-release`:

```bash
helm install my-release . -f values.yaml
```

You can override the default values by creating your own `values.yaml` file or by using the `--set` flag. For example:

```bash
helm install my-release . --set global.clusterName=my-cluster
```

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.
