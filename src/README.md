# Extended Universal Developer Image (UDI) for OpenShift DevSpaces

## Extending UDI
 
The [`Containerfile`](./Containerfile) included in this repo demostrates how to extend the official UDI image with extra tooling for Red Hat OpenShift DevSpaces.

## Building the Image

Build the image and push it to quay.io for instance:
> **NOTE**: Use the appropriate image repository namespace according to your quay environment.

```
podman build -t quay.io/mmuth/devspaces-extended-udi:3.21 .
podman push quay.io/mmuth/devspaces-extended-udi:3.21
```

## Using the New Image

To use this new UDI image in your own workspaces, specify the image location as the `image` in the `tools` component of your [devfile](../devfile.yaml).

When your workspace starts up, it will be using your extended UDI image.