pipeline {

   agent any
    environment {
        DOCKER_USERNAME = credentials('DOCKER_USERNAME')
 
    }
   stages {

       stage('docker-compose') {
           steps {
              sh "docker-compose down || true"
              sh "docker system prune -a -f"
              sh "docker-compose --verbose up -d"
              sh "ls -ltra"
           }
       }
      
       stage('docker-login-push') {
           steps {
              sh "echo $DOCKER_USERNAME_PSW | docker login --username $DOCKER_USERNAME_USR --password-stdin"
              sh "docker image tag postgres:11 popedaniels/postgres:latest"
              sh "docker push popedaniels/postgres:latest"
           }
       }
   }
   post {
      always {
         sh "docker system prune -a -f"
         sh "docker-compose ps"
      }
   }   
}
