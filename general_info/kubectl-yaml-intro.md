# YAML Manifests with Kubernetes

## Overview

Kubernetes supports several methods for creating and managing resources, one of which is through YAML manifests. YAML manifests are configuration files that define the desired state of Kubernetes resources such as Pods, Deployments, Services, etc. These files are then applied to the cluster using tools like `kubectl` to create and manage the resources defined within them.

## YAML Manifests vs Interactive kubectl Commands

### YAML Manifests

1. **Declarative Approach**: YAML manifests represent a declarative approach to configuration, where the file defines the desired state of the resource. The Kubernetes system reads the manifest file and works to make the cluster's current state match the desired state defined in the manifest.

2. **Version Control**: Since YAML files are text-based, they can be stored in version control systems (such as Git). This allows for versioning, auditing, and rollback of configurations, which is crucial for maintaining the integrity of cluster configurations over time.

3. **Reusability and Sharing**: YAML files can be easily shared among team members, reused in different environments, or published for community use. This promotes collaboration and consistency across deployments.

4. **Batch Changes**: With YAML, you can define multiple resources in a single file or across multiple files, and apply all those changes in a batch by applying the directory or files. This is efficient for managing multiple resources collectively.

### Interactive kubectl Commands

1. **Imperative Approach**: Interactive `kubectl` commands are imperative, which means they perform operations in real-time and modify the cluster state directly. This approach is more about performing actions than defining states.

2. **Instant Feedback**: When using `kubectl` commands interactively, you get immediate feedback about the operation's success or failure. This can be beneficial for debugging or when immediate results are necessary.

3. **Suitable for Ad-hoc Changes**: Interactive commands are ideal for making quick, ad-hoc changes to your cluster, such as scaling a deployment or debugging a particular pod.

4. **No Version Control**: Commands executed interactively are not stored in a version control system directly, which might lead to inconsistencies if not tracked properly.

## Examples of Using the `kubectl` Tool

### 1. `kubectl describe pod`

This command provides detailed information about a specific pod. It includes the status, conditions, events, and other relevant metadata.

**Example Usage:**
```bash
kubectl describe pod my-pod
```
Replace `my-pod` with the name of the pod you want to inspect.

### 2. `kubectl get pods` and `kubectl get pods -o yaml`

These commands list all the pods in the current namespace. Adding `-o yaml` outputs the information in YAML format, which is useful for debugging or saving configurations.

**Example Usage:**
```bash
kubectl get pods
kubectl get pods -o yaml
```

### 3. `kubectl delete pod`

This command deletes a pod from your cluster. It is crucial for cleaning up resources or resetting the state of your deployment.

**Example Usage:**
```bash
kubectl delete pod my-pod
```
Replace `my-pod` with the name of the pod you want to delete.

### 4. `kubectl edit pod`

This command opens the configuration of a pod in an editor. This allows you to make changes to the pod’s configuration directly and apply them live to the cluster.

**Example Usage:**
```bash
kubectl edit pod my-pod
```
Replace `my-pod` with the name of the pod you wish to edit. Save and close the editor to apply changes.

### 5. `kubectl apply -f manifest.yaml`

This command applies a configuration to a resource from a file. It is commonly used for creating or updating resources in your cluster based on a YAML file.

**Example Usage:**
Define the pod in a YAML file, `pod.yaml`:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  namespace: default
spec:
  containers:
  - image: nginx
    imagePullPolicy: Always
    name: nginx
```

Apply the pod with `kubectl`:

```bash
kubectl apply -f pod.yaml
```

### Scaling a Deployment with kubectl Command

1. Edit the pod interactively:

    ```bash
    kubectl edit pod nginx-deployment
    ```

## Recap

Using YAML manifests provides a structured, version-controlled method for managing Kubernetes resources and is suitable for maintaining consistent configurations across environments. On the other hand, interactive `kubectl` commands are useful for quick modifications and immediate feedback. Both methods have their place in a well-rounded Kubernetes workflow.

## Useful Links

Here are some resources that can help you dive deeper into using YAML manifests with Kubernetes and understanding kubectl commands:

1. **Kubectl Cheat Sheet**: A quick reference guide for commonly used kubectl commands which can be handy while working with Kubernetes clusters.
   - [Kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/quick-reference/)

2. **Kubectl Commands Reference**: Detailed reference guide for all kubectl commands, options, and usage.
   - [Kubectl Commands](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)

3. **Learn YAML**: Understanding the basics of YAML syntax can be very helpful when writing and troubleshooting YAML manifests.
   - [Learn YAML in Y Minutes](https://learnxinyminutes.com/docs/yaml/)

5. **Kubernetes YAML File Generator**: An online tool to generate Kubernetes YAML files for basic resources quickly.
   - [Kubernetes YAML Generator](https://k8syaml.com/)

6. **YAML basics and usage in K8S**: A tutorial to learn the structure of YAML and the basics of how to write a YAML file and explore an example YAML file that's used in Kubernetes.
   - [K8S YAML basics](https://developer.ibm.com/tutorials/yaml-basics-and-usage-in-kubernetes/)
