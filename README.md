

# NodeMsMonorepo
 
  

#### Install the following

- docker
- kubectl
- minikube
- virtualbox

<br/><br/>

#### Install on mac

```shell
brew update
brew install kubectl
brew cask install docker
brew cask install minikube
brew cask install virtualbox
```
<br/><br/>

#### Check if installed properly 

```shell
kubectl version --client
docker --version
docker-compose --version
docker-machine --version
minikube version
```
<br/><br/>

### Run docker desktop

Open docker desktop standalone app  <br/><br/><br/>



### Start the kubernetes cluster with minikube (minikube is local Kubernetes)

```shell
minikube start
```
<br/><br/>

#### Check if minikube node is ready
```shell
kubectl get nodes
```
<br/>

You should see something like that
``` text
NAME       STATUS    ROLES     AGE       VERSION
minikube   Ready     master    40s        v1.14.0
```
<br/>

### Build docker images of our microservices

You can run the following commands with you NX IDE extension (vscode or intellij)

```shell
nx run svc-cart:dockerBuild

nx run svc-products:dockerBuild

nx run svc-user:dockerBuild
```
<br/>

Check whether docker images has been created
```shell
docker images --format "table {{.ID}}\t{{.Tag}}\t{{.Repository}}"
```
You should see something like that
```shell
IMAGE ID       TAG       REPOSITORY
9d280d1feec7   latest    svc-user
01a97cac7c74   latest    svc-products
73de4fa41b44   latest    svc-cart
8768eddc4356   v0.0.25   gcr.io/k8s-minikube/kicbase

```

### Run minikube docker daemon
```shell
eval $(minikube docker-env)
```
<br/>



