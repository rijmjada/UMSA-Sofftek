* Crear una red net_jenkins donde vamos a correr todo
* Crear el volumen persistente donde vamos a guardar la data de Jenkins
* Bajar la imagen de jenkins
* Correr la imagen teniendo en cuenta de agregar la red y el volumen

//////////////////////
Solución:

docker network create net_jenkins

docker volume create jenkins_data

docker pull jenkins/jenkins

docker run -d `
  --name jenkins_container `
  -p 8080:8080 `
  -p 50000:50000 `
  --network net_jenkins `
  -v jenkins_data:/var/jenkins_home `
  jenkins/jenkins


password: 
docker exec -it jenkins_container cat /var/jenkins_home/secrets/initialAdminPassword
///////////////////////



* Crear los volumenes que necesita sonarqube, crear 3 aunque podrian estar en un mismo disco

docker volume create --name sonarqube_data
docker volume create --name sonarqube_logs
docker volume create --name sonarqube_extensions

* Utilizar la misma red de jenkins

* Bajar la imagen

/////////////////////
Solucion:


docker volume create --name sonarqube_data
docker volume create --name sonarqube_logs
docker volume create --name sonarqube_extensions


docker pull sonarqube

docker run -d `
  --name sonarqube_container `
  -p 9000:9000 `
  -p 9092:9092 `
  --network net_jenkins `
  -v sonarqube_data:/opt/sonarqube/data `
  -v sonarqube_logs:/opt/sonarqube/logs `
  -v sonarqube_extensions:/opt/sonarqube/extensions `
  sonarqube
