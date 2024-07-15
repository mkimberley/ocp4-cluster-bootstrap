# Bootstraps a OCP cluster on GCP

## Provisions:

* Machine Sets in 3 AZs
* Machine Autoscalers in 3 AZs
* htpasswd auth provider
* Microsoft Entra ID Auth provider
* GitHub IDP Auth provider

## How to use:

* Clone this repository in your own environment

### Create the following files with the relevant secret iformation:

* files/githubidp-secret
* files/htpasswd-file
* files/openid-secret

### Updated the following file:

* values.yaml

### Manually Add Required Labels and Annotations:


```bash
oc edit oauth cluster
```

Then, add the following labels and annotations under metadata:

```yaml
metadata:
  labels:
    app.kubernetes.io/managed-by: "Helm"
  annotations:
    meta.helm.sh/release-name: "cluster-bootstrap"
    meta.helm.sh/release-namespace: "<namespace>"
```

You will additionally need to do this to any existing machinesets that you wish to manage with this chart.

Install the helm chart:

```bash
helm install <chart-name> cluster-bootstrap/ --namespace <namespace>
```