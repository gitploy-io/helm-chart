# Gitploy Installation

## Disclaimer

This page is not intended to be a comprehensive guide to installing Gitploy. It will only cover the Kubernetes-specific parts of the process.

## Configuration 

In order to install the chart, you'll need to pass in additional configuration. This configuration comes in the form of Helm values, which are key/value pairs.

```yaml
env: 
  # REQUIRED: Set the user-visible hostname.
  #
  GITPLOY_SERVER_HOST: ""
  # REQUIRED: The protocol to pair with the value in GITPLOY_SERVER_HOST (http or https).
  #
  GITPLOY_SERVER_PROTO: https

  # Slack-specific variables.
  #
  GITPLOY_SLACK_CHANNEL:
  GITPLOY_SLACK_CLIENT_ID:
  GITPLOY_SLACK_CLIENT_SECRET:
```

Copy these into a new file, which we'll call `values.overrides.yaml`. Adjust the included defaults to reflect your environment.

## Run the installation

Create the namespace to install gitploy if it does not already exist:

```console
kubectl create ns gitploy
namespace/gitploy created
```

Run `helm` install with your values provided:

```console
helm install --namespace gitploy gitploy gitployio/gitploy  -f values.overrides.yaml
```

Once the install command is ran, your Kubernetes cluster will begin creating resources. To see how your deploy is shaping up, run:

```console
$ kubectl --namespace gitploy get pods
NAME                                 READY   STATUS    RESTARTS   AGE
gitploy-76d6bb8968-3d5n9               1/1     Running   0          2m
```
