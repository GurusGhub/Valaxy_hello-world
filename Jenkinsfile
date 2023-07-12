pipeline{
    agent any
     tools { 
        maven 'maven' 
    }
    stages{
        stage("Git Checkout"){
            steps{
           git credentialsId: 'GurusGhub', url: 'https://github.com/GurusGhub/Valaxy_hello-world.git'
            }
        }
        stage("Maven Build"){
            steps{
                sh "mvn clean install"
            }
        }
   /*   stage("Deploy to tomcat"){
            steps{
                sshagent(['Deploy_user']) {
                sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@172.31.87.199:/opt/tomcat/webapps"
               
               }
            }
        } */
      stage('Static Code Analysis') {
      environment {
        SONAR_URL = "http://100.24.113.214:9000"
      }
      steps {
        withCredentials([string(credentialsId: 'sonarqube', variable: 'SONAR_AUTH_TOKEN')]) {
          sh 'cd Valaxy_hello-world && mvn sonar:sonar -Dsonar.login=$SONAR_AUTH_TOKEN -Dsonar.host.url=${SONAR_URL}'
        }
      }
    }
  }
}
