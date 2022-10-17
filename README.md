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
5- Display all the pods in the vault namespace.

```bash
kubectl get pods -n vault
```
```sh
NAME                                    READY   STATUS    RESTARTS   AGE
vault-0                                 1/1     Running   0          3h8m
vault-agent-injector-59775cb565-8xrmc   1/1     Running   0          3h8m
```

# Create Vault Secret

1- Execute bellow command to interactive shell session on the vault-0 pod.

```bash
kubectl exec vault-0 -n vault -it – bin/sh
```

2- Create new secret engine path.

```bash
vault secrets enable -path=<path name> kv # e.g. nginx-secret
```

```bash
vault secrets enable -path=nginx-secret kv 
```

3- Check the engine version is set to version 2

   - First disable the secret engine.

    ```bash
    vault secrets disable <path name> kv # e.g. nginx-secret
    ```
        ```bash
    vault secrets disable nginx-secret
    ```
    
   - Second set version 2 and enable secret engine
  
    ```bash
    vault secrets enable -version=2 -path=<path name> kv # e.g. nginx-secret
    ```
    
    ```bash
    vault secrets enable -version=2 -path= nginx-secret kv 
    ```











