# Gitploy Helm Charts

This repository hosts official Helm charts for Gitploy. These charts are used to deploy Gitploy to Kubernetes.

## Install Helm

Read and follow the Helm installation guide.

## Add the Gtiploy Helm Chart repo

In order to be able to use the charts in this repository, add the name and URL to your Helm client:

```console
$ helm repo add gitployio https://gitploy.io/helm-chart/
$ helm repo update
```

## Installing Gitploy

See the [Gitploy Installation](./docs/install.md).

## Configuring Gitploy

See [values.yaml](./charts/gitploy/values.yaml) to see the Chart's default values. 

To adjust an existing Gitploy install's configuration:

```console
# If you have a values file:
$ helm upgrade gitploy gitployio/gitploy --namespace gitploy --values values.overrides.yaml
# If you want to change one value and don't have a values file:
$ helm upgrade gitploy gitployio/gitploy --namespace gitploy --reuse-values --set someKey=someVal
```

## Upgrading Gitploy

Read the release notes to make sure there are no backwards incompatible changes.  Make adjustments to your values as needed, then run `helm upgrade`.


```console
# This pulls the latest version of the gitploy chart from the repo.
$ helm repo update
$ helm upgrade gitploy gitployio/gitploy --namespace gitploy --values values.overrides.yaml
```

## Uninstalling Gitploy

To uninstall/delete the `gitploy` deployment in the `gitploy` namespace:

```console
$ helm delete gitploy --namespace gitploy
```

## Documentation

See the Gitploy documentation site for more information.

## License

BSD 3-Clause License
