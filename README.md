# pep-restaurant-local-env

### How to run containers

* Firstly build each container
    docker-compose build [CONTAINER]

* Run Container
    docker-compose up -d [CONTAINER]

### Notes

* Sonarqube on WINDOWS needs to run cmd:
    wsl -d docker-desktop
    sysctl -w vm.max_map_count=262144
  
