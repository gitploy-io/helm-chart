# Gitploy Installation

## Disclaimer

This page is not intended to be a comprehensive guide to installing Gitploy. It will only cover the Kubernetes-specific parts of the process.

## Configuration 

To install the chart, you'll need to pass in an additional configuration. This configuration comes in the form of Helm values, which are key/value pairs.

```yaml
env: 
  # REQUIRED: Set the user-visible hostname.
  #
  GITPLOY_SERVER_HOST: ""
  # REQUIRED: The protocol to pair with the value in GITPLOY_SERVER_HOST (http or https).
  #
  GITPLOY_SERVER_PROTO: https

  # REQUIRED: Identity users as admin.
  #
  GITPLOY_ADMIN_USERS: ""

  # Github-specific variables.
  #
  # REQUIRED: Github oAuth client id.
  #
  GITPLOY_GITHUB_CLIENT_ID: ""
  # REQUIRED: Github oAuth client secret.
  #
  GITPLOY_GITHUB_CLIENT_SECRET: ""
```

Copy these into a new file, which we'll call `values.overrides.yaml`. Adjust the included defaults to reflect your environment.

## Run the installation

Create the namespace to install Gitploy if it does not already exist:

```console
kubectl create ns gitploy
namespace/gitploy created
```

Run `helm` installs with your values provided:

```console
helm install --namespace gitploy gitploy gitployio/gitploy  -f values.overrides.yaml
```

Once the install command is run, your Kubernetes cluster will begin creating resources. To see how your deploy is shaping up, run:

```console
$ kubectl --namespace gitploy get pods
NAME                                 READY   STATUS    RESTARTS   AGE
gitploy-76d6bb8968-3d5n9               1/1     Running   0          2m
```

## Upgrading Gitploy

Read the release notes to make sure there are no backward-incompatible changes. Make adjustments to your values as needed, then run `helm upgrade`.


```console
# This pulls the latest version of the gitploy chart from the repo.
helm repo update
helm upgrade gitploy gitployio/gitploy --namespace gitploy --values values.overrides.yaml
```

## Uninstalling Gitploy

To uninstall/delete the `gitploy` deployment in the `gitploy` namespace:

```console
helm delete gitploy --namespace gitploy
```

