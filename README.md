# Vault Installation Guide

I am using the [Helm-Chart](https://www.vaultproject.io/docs/platform/k8s/helm) to run vault on kubernetes.

1- Add the HashiCorp Helm repository.

```bash
helm repo add hashicorp https://helm.releases.hashicorp.com
```
2- Update all repositories to latest versions.

```bash
helm repo update
```

3- Create namespace vault.

```bash
kubectl create namespace vault
```

4- Install the latest version of the Vault server running in development mode.

```bash
helm install vault hashicorp/vault --set='server.dev.enabled=true' -n vault
```
