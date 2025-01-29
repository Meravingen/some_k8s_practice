# Introduction to Kubernetes ReplicaSets

ReplicaSets are a fundamental workload controller in Kubernetes that ensure a specified number of identical Pod replicas are running at any given time. Essentially, a ReplicaSet's purpose is to maintain a stable set of replica Pods running at any desired time. This is particularly useful for ensuring the availability and scalability of your application.

ReplicaSets replace the older ReplicationControllers but offer more expressive pod selectors and no functional differences in terms of orchestrating pod lifecycles. They are often used with Deployments to facilitate updates and rollbacks, although they can be used standalone for maintaining a constant number of Pods.

For a deeper understanding of ReplicaSets and their role in Kubernetes workload management, you can visit the [Kubernetes ReplicaSets Documentation](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/).

## Task: Identify the Error in the Kubernetes ReplicaSet Manifest

The provided Kubernetes manifest is intended to create a ReplicaSet that manages two replicas of a Pod running the nginx image. However, there are errors in the manifest. Your task is try to apply this manifest, pinpoint the incorrect configuration, and suggest the appropriate corrections.

Here is the manifest for your review:

```yaml
apiVersion: v1
kind: ReplicaSet
metadata:
  name: replicaset-1
spec:
  replicas: 2
  selector:
    matchLabels:
      tier: frontend
  template:
    metadata:
      labels:
        tier: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
```

## Task: Increase the Number of Replicas in a Kubernetes ReplicaSet

This task involves increasing the number of replicas in a Kubernetes ReplicaSet to demonstrate two approaches: using interactive `kubectl` commands and updating the YAML manifest.

## Objectives
1. Increase the number of replicas from 2 to 5.
2. Perform this change using both interactive `kubectl` commands and by modifying the YAML manifest.

## Method 1: Interactive `kubectl` Commands

### Using `kubectl scale`
You can directly scale the number of replicas in a ReplicaSet using the `kubectl scale` command. This method is quick and suitable for straightforward scaling operations.

```bash
kubectl scale replicaset replicaset-1 --replicas=5
```

### Using `kubectl edit`
Alternatively, you can manually edit the ReplicaSet configuration in an interactive editor by using `kubectl edit`. This method opens the manifest in an editor, allowing you to make various modifications beyond just scaling.

```bash
kubectl edit replicaset replicaset-1
```
In the editor, change the `replicas` value from 2 to 5, save, and exit the editor to apply the changes.

## Method 2: YAML Manifest Correction and Applying it

1. **Modify the YAML Manifest**: Open the existing YAML file defining the ReplicaSet, and change the `replicas` field from 2 to 5.

Here's the updated section of the manifest:
```yaml
spec:
  replicas: 5
  selector:
    matchLabels:
      tier: frontend
  template:
    metadata:
      labels:
        tier: frontend
    spec:
      containers:
      - name: nginx
        image: nginx
```

2. **Apply the Updated Manifest**: After saving your changes to the YAML file, apply the updated configuration to your cluster using `kubectl apply`.

```bash
kubectl apply -f <path-to-updated-replicaset-yaml>
```
