# Kubernetes

At Reevoo our core infrastrucure is (slowly) moving to Kubernetes. This is a quick guide to getting your workstation setup to work with our clusters.

## Installing Tools (OSX)

### `kubectl` is the standard cli tool for Kubernetes

```
brew install kubernetes-cli
```

### `helm` is a Kubernetes package manager.


```
brew install kubernetes-helm
```

While not yet in use we will shortly be using Helm to deploy our applications to kubernetes clusters.

### `minikube` (Optional)

Minikube allows you to run a local Kubernetes cluster, for learning about Kubernetes or running your development environment.
Hombrew does not have a package for minikube as it is distrabuted as a binary, However it can be installed with [Homebrew Cask](https://caskroom.github.io/)

You can discover more about using minikube [here](https://github.com/kubernetes/minikube).

```
brew tap caskroom/cask
brew cask install minikube
```

## Configuring `kubectl`

`kubectl` is configured with a file found at `~/.kube/config`. This configuration is also used by Helm.

To get the correct config for our legacy cluster (used for all projects at this time) contact devops.

For access to the newer cluster(s) you will be issued with a token and the name of a cluster.

Here is an example of setting up access to a fictional cluster called `jelly-bowl`.

```bash
K8S_CLUSTER_NAME=jelly-bowl
K8S_TOKEN=thisismytokenthisismyperfecttoken

kubectl config set-cluster ${K8S_CLUSTER_NAME} --server=https://${K8S_CLUSTER_NAME}.kubernetes.reevoocloud.com
kubectl config set-credentials $(whoami) --token=${K8S_TOKEN}
kubectl config set-context ${K8S_CLUSTER_NAME} --cluster=${K8S_CLUSTER_NAME} --user=$(whoami)
kubectl config use-context ${K8S_CLUSTER_NAME}
```
