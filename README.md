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
vault secrets enable -version=2 -path=nginx-secret kv 
```

4- Create a secret path with a Key/Value

```bash
vault kv put <path name>/<path secret> key=value key=value #e.g. path name:(nginx-secret) path secret:(config) key & value username="nginx-user" password="nginx-password"
```

```bash
vault kv put nginx-secret/config username="nginx-user" password="nginx-password"
```

5- Execute bellow command to retrieve your registered secrets

```bash
vault kv get <path name>/<path secret> #e.g. nginx-secret/config
```

```bash
vault kv get nginx-secret/config
```

# Create Vault Policy

We need to move from Back slash-"/ $" root to Telda-"~ $" inside pod interactive shell (bin/sh) to create ("nginx-policy.hcl") file and add the bellow inside this file then save.




















