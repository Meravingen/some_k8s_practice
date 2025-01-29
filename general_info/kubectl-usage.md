# Kubectl Usage Documentation(to be completed)

Kubectl is a command-line tool that allows you to run commands against Kubernetes clusters. You can use kubectl to deploy applications, inspect and manage cluster resources, and view logs.

## Table of Contents
- [Getting Started](#getting-started)
- [Common Commands](#common-commands)
  - [Get Pods](#get-pods)
  - [Create Resources](#create-resources)
  - [Extracting Data from Secrets](#extracting-data-from-secrets)

## Getting Started

Before you can use kubectl, you need to have a Kubernetes cluster, and the kubectl command-line tool must be configured to communicate with your cluster. You can check if kubectl is configured properly by running the following command, which should return information about your cluster:

```bash
kubectl cluster-info
```

## Common Commands

### Get Pods

To get information about pods and watch for changes in real-time, you can use the `-w` or `--watch` flag with the `get pods` command:

```bash
kubectl get pods -w
```

This command will continuously monitor the pods' status and update the output as changes occur.

### Create Resources

To create resources in a dry-run mode and output the resource in YAML format, you can use the `--dry-run=client` and `-o yaml` flags with the `create` command. This is useful for validating resource definitions without actually applying them.

For example, to create a deployment in dry-run mode:

```bash
kubectl create deployment my-deployment --image=nginx --dry-run=client -o yaml
```

This command will output the deployment definition in YAML format without actually creating the deployment in the cluster.

### Extracting Data from Secrets

To extract specific data from Kubernetes secrets, you can use the `jsonpath` option. This allows you to parse JSON data and extract only the necessary information.

For example, to extract the username from a secret named `my-secret`:

```bash
kubectl get secret my-secret -o jsonpath='{.data.username}' | base64 --decode
```

This command retrieves the username field from the `my-secret` secret, decodes it from base64, and prints it.

