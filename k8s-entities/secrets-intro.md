# Introduction to Kubernetes Secrets

Kubernetes Secrets are a way to store and manage sensitive information, such as passwords, OAuth tokens, and SSH keys. Using Secrets can help you manage sensitive data more securely, especially in comparison to storing sensitive data in your Pod specifications or in Docker images.

## Overview of Kubernetes Secrets

According to the [Kubernetes documentation](https://kubernetes.io/docs/concepts/configuration/secret/), Secrets are intended to hold sensitive information. Pods can consume Secrets as environment variables, command-line arguments, or as configuration files in a volume.

A Secret is only sent to a node if a Pod on that node requires it. Kubernetes keeps Secrets in a temporary storage on a node, which is a tmpfs volume that is erased when the node is restarted. At rest on the master, Secrets are stored as plaintext in etcd; however, it is possible to configure etcd to encrypt this data at rest.

Here are some key features of Kubernetes Secrets:

- **Security**: Secrets are stored in tmpfs on nodes, reducing the risks of disk-based attacks.
- **Management**: Secrets can be managed independently of the Pods that use them. This separation of concerns can lead to more controlled updates and management of sensitive data.
- **Flexibility**: Secrets can be used in multiple ways - as files in a volume mounted on one or more of a Pod's containers, or used by kubelet when pulling images for the Pod.
- **Confidentiality**: Kubernetes tries to reduce the risk of secret exposure by avoiding writing Secrets to nonvolatile storage, except when explicitly required by the application.

## Task: Identify and Correct Secret used to provide data to env variables

In this example, we'll create a Secret to store database credentials and use it in a Pod to set environment variables.
Kubernetes secret manifest and a pod manifest are intentionally configured with mistakes. Your task is to identify and correct these mistakes

1. **Create a Secret**

First, create a Secret to store the database username and password:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-secrets
type: Opaque
data:
  username: ZGJ1c2VyCg==
  password: cGFzc3dvcmQK
  extra: extraValue==
```

Save this as `db-secrets.yaml` and create the Secret using:

```bash
kubectl apply -f db-secrets.yaml
```

2. **Create a Pod that uses the Secret**

Next, create a Pod that uses the Secret to set environment variables:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: ubuntu-pod
spec:
  containers:
  - name: ubuntu-container
    image: ubuntu
    command: ["sh", "-c", "sleep infinity"]
    env:
    - name: DB_USERNAME
      valueFrom:
        secretKeyRef:
          name: db-secrets
          key: username
    - name: DB_PASSWORD
      valueFrom:
        secretKeyRef:
          name: db-secrets
          key: passwd
    - name: EXTRA_VALUE
      valueFrom:
        secretKeyRef:
          name: db-secrets
          key: extra
```

Save this as `ubuntu-pod.yaml` and create the Pod using:

```bash
kubectl apply -f ubuntu-pod.yaml
```


## Task 2: Identify and Correct secret used as Volume Mount in a Pod

In this example, we'll mount a Secret as a volume in a Pod. This is useful when your application expects to read credentials from a file rather than environment variables.
Both manifests contain several intentional mistakes. Your task is to review the manifests, identify the mistakes, and correct them.

1. **Create secret from the following manifest**

   If you haven't created the `db-secrets` Secret, refer to previous task to create it.

2. **Create a Pod that mounts the Secret as a volume**

   Here's how to mount the Secret as a volume:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: ubuntu-pod
spec:
  containers:
  - name: ubuntu-container
    image: ubuntu
    tty: true
    stdin: true
    volumeMounts:
    - name: secret-volume
      mountPath: /etc/secret
      readOnly: true
  volumes:
  - name: secret-volume
    secret:
      secretName: db-secret
```

Save this as `ubuntu-pod-volume.yaml` and create the Pod using:

```bash
kubectl apply -f ubuntu-pod-volume.yaml
```
