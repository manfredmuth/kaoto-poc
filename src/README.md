# Extended Universal Developer Image (UDI) for OpenShift DevSpaces

## Extending UDI
 
The [`Containerfile`](./Containerfile) included in this repo demostrates how to extend the official UDI image with extra tooling for Red Hat OpenShift DevSpaces.

Instead of installing jBang when starting up your workspace you will have jBang already built into your image which
a - helps to speed up starttime
b - would leave you with a specific version in your image and you would need to implement a lifecycle process for your image

## Building the Image

Build the image and push it to quay.io for instance:
> **NOTE**: Use the appropriate image repository namespace according to your quay environment.

```
podman build -t quay.io/mmuth/devspaces-extended-udi:3.21 .
podman push quay.io/mmuth/devspaces-extended-udi:3.21
```

## Using the New Image

To use this new UDI image in your own workspaces, specify the image location as the `image` in the `tools` component of your [devfile](../src/devfile.yaml).

And you would need to move this devfile.yaml to the [root directory](../)

When your workspace starts up, it will be using your extended UDI image. Which contains the jBang installation.

In this [devfile.yaml](./devfile.yaml) you find a section like this:

```
commands:
  - id: post-start-install-extensions
    exec:
      label: "Install Apache Camel and Kaoto extensions"
      component: vscode
      commandLine: >
        code --install-extension redhat.apache-camel-extension-pack &&
        code --install-extension redhat.vscode-kaoto
      workingDir: /projects
```

Which is an alternative to install the VS Code extensions and you miss here the jBang installation as you saw it in [../devfile.yaml](../devfile.yaml)
