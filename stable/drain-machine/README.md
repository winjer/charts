# Drain Machine

[Drain Machine](https://github.com/isotoma/drain-machine) is a daemon to monitor AWS EC2 lifecycle events with the intention of cordoning and draining a node before it is abruptly terminated by AWS. It watches for pending terminations due to Autoscaling Group changes or because of impending spot instance termination.

## Introduction

This chart creates the resources necessary to run drain-machine on your cluster, using the [Helm](https://helm.sh) package manager.

## Installation

To install the chart with the release name `my-release`, run:

```bash
helm install --name my-release incubator/drain-machine
```

## Uninstall

To uninstall/delete the `my-release` deployment:

```bash
helm delete my-release
```

## Configuration

The following table lists the configurable parameters of the Drain Machine chart and its default values.

You must set `drain.cluster` to a valid value. This should be the name of the cluster in the kubernetes.io/cluster/NAME tag applied to your autoscaling groups. See the drain-machine documentation for details.

Also don't forget to add any tolerations required to ensure drain-machine runs on all your nodes!

| Parameter | Description | Default |
| --------- | ----------- | ------- |
| `drain.cluster` | The name of the cluster to drain | |
| `image.repository` | docker image | `"quay.io/isotoma/drain-machine"` |
| `image.tag` | version | `"stable"` |
| `image.pullPolicy` | pull policy | `"IfNotPresent"` |
| `resources` | pod resources | `{}` |
| `nodeSelector` | optional settings | `{}` |
| `tolerations` | optional settings | `[]` |
| `affinity` | session affinity | `{}` |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
$ helm install --name my-release incubator/drain-machine
```

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml incubator/drain-machine
```
