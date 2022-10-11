# Notes for code-engine

## Via a Container

Build the container:

```bash
docker build -t quay.io/jjasghar/kubecon22-code-engine:latest .
```

Push the container:

```bash
docker push quay.io/jjasghar/kubecon22-code-engine:latest
```

Note: don't forget to make the container public.

## Set up

Target the correct resource group:

```bash
ibmcloud target -g "Default"
```

Target the project:

```bash
ibmcloud ce project select -n kubecon22-code-engine
```

## Via local code and build packs

Build via the source

```bash
ibmcloud ce app create --name kubecon22-code-engine --build-source . --strategy buildpacks
```

## Via Container we built at the beginning

Create the application: `-nw` will not wait

```bash
ibmcloud ce application create --name kubecon22-code-engine --image quay.io/jjasghar/
kubecon22-code-engine:latest
```

## Investigating the app

Get some info:

```bash
ibmcloud ce application get --name kubecon22-code-engine
```

Spinning up "5" min instances:

```bash
ibmcloud ce application update --name kubecon22-code-engine --min 5
```

Going back to zero instances:

```bash
ibmcloud ce application update --name kubecon22-code-engine --min 0 -nw
```

## Rolling update

Update the container:

```bash
docker build -t quay.io/jjasghar/kubecon22-code-engine:latest .
docker push quay.io/jjasghar/kubecon22-code-engine:latest
ibmcloud ce application update --name kubecon22-code-engine
```

## Clean up

Delete the application:

```bash
ibmcloud ce application delete --name kubecon22-code-engine
```
