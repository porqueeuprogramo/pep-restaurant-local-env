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