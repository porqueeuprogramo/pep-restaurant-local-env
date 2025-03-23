# pep-restaurant-local-env

- A simple environment to supply our pep-restaurant using mostly [Java](https://java.com) and [Maven](https://maven.apache.org/).
- It has also an API RestFul
- The purpose of the application is also a non-monolithic architecture.

```
To ensure those environment will work correctly, you must have all repositories bellow cloned:
```
[pep-keycloak](https://github.com/porqueeuprogramo/pep-keycloak)
[pep-restaurant-ms-manager](https://github.com/porqueeuprogramo/pep-restaurant-ms-manager)
[pep-restaurant-ms-bff](https://github.com/porqueeuprogramo/pep-restaurant-ms-bff)
## Deploy sonarqube on Windows

```bash
# Command line required on WINDOWS:
$ wsl -d docker-desktop sysctl -w vm.max_map_count=262144  

# Add 127.0.0.1 IP to a hosts file (C:\Windows\System32\drivers\etc\hosts) to make sure that you have access keycloak administration

#Sonarqube user and password (you will be asked to change the password on the first login)
$ username=admin
$ password=admin

# Firstly build pep-keycloak container (tagged container)
$ docker-compose build -t pep-keycloak
```
## Deploy the environment up
```bash
# Run 'docker-compose.yml' which has some configuration for what you need and to build and deploy the necessary containers
$ docker-compose up -d 
```

# Local Development

## Kubernetes

### Setup

#### Setup Kubernetes cluster

Activate Kubernetes in the Docker Desktop settings

#### Install the Kubernetes UI
https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/

- Change kubectl context to Docker Desktop
```
kubectl config use-context docker-desktop
```
- Install the image for Kubernetes Dashboard
```
helm repo add kubernetes-dashboard https://kubernetes.github.io/dashboard
```
```
helm upgrade --install kubernetes-dashboard kubernetes-dashboard/kubernetes-dashboard --create-namespace --namespace kubernetes-dashboard
```
```
kubectl -n kubernetes-dashboard port-forward svc/kubernetes-dashboard-kong-proxy 8443:443
```
The Kubernetes Dashboard should be available at
**https://localhost:8443**


#### Create an admin user for the Kubernetes Dashboard
https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md

````
kubectl apply -f kubernetes/dashboard-adminuser.yaml
````
```
kubectl apply -f kubernetes/admin-cluster-role-binding.yml
```

#### Get the Bearer Token for the admin user

```
kubectl -n kubernetes-dashboard create token admin-user
```

helm upgrade --install pep-restaurant-ms-manager kubernetes --set app.properties.content=default -- set image.tag=latest -f kubernetes/values/emea/values-test.yaml --namespace=default


