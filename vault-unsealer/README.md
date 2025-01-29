# Vault Unsealer Helm Chart

This Helm chart deploys a set of Kubernetes resources to automatically initialize and unseal HashiCorp Vault. It provides:

- A Deployment that continuously checks if Vault pods are sealed, automatically unsealing them.
- A Job to initialize Vault if it isn’t already.
- A second Job (optional) to apply bootstrap configurations (e.g., auth methods, policies, roles) to be used with [vault-config-operator](https://github.com/redhat-cop/vault-config-operator).

## Installation

```shell
helm install vault-unsealer ./vault-unsealer
```

## Configuration

Most settings can be customized in values.yaml. Some key parameters:

`namespace`: Overrides the chart installation namespace.
`vaultReleaseName`: Identifies the Vault pods to unseal.
`serviceAccount.create`: Creates a ServiceAccount if needed.
`bootstrap.enabled`: Toggles the Vault bootstrap job.
`image`: Defines the Docker image to use for the init/unsealer jobs.
`resources`: Allocates CPU/memory resources.

## Unseal

The unsealer container checks each Vault pod’s seal status and, if sealed, applies all provided unseal keys.

## Bootstrap

If bootstrap.enabled is true, a separate job applies additional Vault configurations (like policies or roles). You can modify these in configmap.yaml.

## License

This Helm chart is provided under the MIT License.
