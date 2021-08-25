

# NodeMsMonorepo
 
  

#### Install the following
- NX
- docker
- kubectl
- minikube
- virtualbox

<br/>

#### Install on mac

```shell
npm install -g nx
brew update
brew install kubectl
brew cask install docker
brew cask install minikube
brew cask install virtualbox
```
<br/>


#### Install on Linux (Debian)

install nx
`npm install -g nx`

To install docker, follow the instructions here:
https://docs.docker.com/engine/install/ubuntu/

Install docker-compose
```
sudo apt install docker-compose
```


Docker Desktop works on Mac and Windows only. A proper alternative is dockstation app:
https://dockstation.io/

To install kubectl follow the instructions here:
https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/

To install minikube follow the instructions here:
https://minikube.sigs.k8s.io/docs/start/

To install virtualbox follow the instructions here:
https://www.virtualbox.org/wiki/Linux_Downloads

<br/>

#### Check if installed properly 

```shell
kubectl version --client
docker --version
docker-compose --version
docker-machine --version
minikube version
```
<br/>

### Run docker desktop

Open docker desktop standalone app  <br/><br/><br/>



### Start the kubernetes cluster with minikube (minikube is local Kubernetes)

```shell
minikube start
```
<br/>

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
<br/>

### Deploy to kubernetes - Run NX commands
You can run the following commands with your IDE's NX extension (vscode or intellij)

```shell
nx run svc-cart:kubernetesDeploy 

nx run svc-products:kubernetesDeploy 

nx run svc-user:kubernetesDeploy 
```
<br/>


### Check if pods are running 

```shell
kubectl get pods
```

```shell
NAME                           READY   STATUS    RESTARTS   AGE
svc-cart-8b6dfcfb4-tzccw       1/1     Running   0          39m
svc-products-5b9d7478b-5r5zq   1/1     Running   0          14m
svc-user-5c59cb6776-gdt2h      1/1     Running   0          5m54s

```
<br/>

### Check if services are running 

```shell
kubectl get services
```


```shell
kubernetes             ClusterIP   10.96.0.1        <none>        443/TCP        18h
svc-cart-service       NodePort    10.99.159.203    <none>        80:32180/TCP   25m
svc-products-service   NodePort    10.105.26.125    <none>        80:30915/TCP   16m
svc-user-service       NodePort    10.102.239.226   <none>        80:32085/TCP   8m13s

```
<br/>
<br/>

### Access services outside the node (minikube is able to create tunnel )

```shell
minikube service svc-cart-service --url
```

<br/>
You will see something like that:

```shell
🏃  Starting tunnel for service svc-cart-service.
|-----------|------------------|-------------|------------------------|
| NAMESPACE |       NAME       | TARGET PORT |          URL           |
|-----------|------------------|-------------|------------------------|
| default   | svc-cart-service |             | http://127.0.0.1:53401 |
|-----------|------------------|-------------|------------------------|
http://127.0.0.1:53401
❗  Because you are using a Docker driver on darwin, the terminal needs to be open to run it.

```

#### Open up `http://127.0.0.1:53401/api`  in your browser

You should see:
```shell
{"message":"Welcome to svc-cart!"}
```

<br/>


#### Open another terminal instance and run another service


==============================================
<br/>
<br/>

### Monitor services with minikube dashboard

run minikube dashboard
```shell
minikube dashboard
```
<img width="1680" alt="Screen Shot 2021-08-25 at 19 59 01" src="https://user-images.githubusercontent.com/88276747/130833667-8e2ea4a4-2687-4e83-ae8d-d1c47fdd29d4.png">

