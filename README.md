

# NodeMsMonorepo
 
  

#### Install the following

- docker
- kubectl
- minikube
- virtualbox


#### Install on mac

```shell
brew update
brew install kubectl
brew cask install docker
brew cask install minikube
brew cask install virtualbox
```

#### Check if installed properly 

```shell
kubectl version --client
docker --version
docker-compose --version
docker-machine --version
minikube version
```


### Start the kubernetes cluster with minikube (minikube is local Kubernetes)

```shell
minikube start
```
