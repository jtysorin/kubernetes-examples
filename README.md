# ConfigMap and Secrets with Volumes Demo

This Kubernetes demo project illustrates how to use ConfigMaps and Secrets as volumes in a Kubernetes Deployment. Specifically, it demonstrates how to configure a Mosquitto MQTT broker with and without these volume types.

## Prerequisites

Before getting started, make sure you have the following prerequisites:

- A running Kubernetes cluster.
- `kubectl` command-line tool installed and configured to access your cluster.

## Project Structure

The project contains the following YAML files:

- `mosquitto-without-volume.yaml`: Deploys a Mosquitto MQTT broker without ConfigMap or Secret volumes.
- `config-file.yaml`: Defines a ConfigMap named `mosquitto-config-file` that contains the Mosquitto configuration.
- `secret-file.yaml`: Defines a Secret named `mosquitto-secret-file` containing a secret file.
- `mosquitto.yaml`: Deploys a Mosquitto MQTT broker with ConfigMap and Secret volumes.

## Usage

### Deploy Mosquitto without Volumes

To deploy Mosquitto without ConfigMap or Secret volumes, apply the following YAML file:

```bash
kubectl apply -f mosquitto-without-volume.yaml
```
You can then access the Mosquitto pod and check its configuration:

```bash
kubectl exec -it <pod-name> -- /bin/sh
cat /mosquitto/config/mosquitto.conf
```

### Deploy Mosquitto with Volumes

To deploy Mosquitto with ConfigMap and Secret volumes, apply the following YAML files:

```bash
kubectl apply -f config-file.yaml
kubectl apply -f secret-file.yaml
kubectl apply -f mosquitto.yaml
```

This will create the necessary ConfigMap and Secret, and deploy Mosquitto with these volumes attached.

You can access the Mosquitto pod and verify the presence of the configuration and secret files:

```bash
kubectl exec -it <pod-name> -- /bin/sh
cat /mosquitto/config/mosquitto.conf
cat /mosquitto/secret/secret.file
```