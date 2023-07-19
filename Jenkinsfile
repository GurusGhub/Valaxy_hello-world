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
      /* environment {
        SONAR_URL = "http://10.0.0.165:9000"
      } */
      steps {
        withsonarQubeEnv('SonarQube9.4'){
          sh "mvn sonar:sonar"
      /*  sh 'mvn clean verify sonar:sonar \
          -Dsonar.projectKey=devsecops_project-key \
          -Dsonar.host.url=http://100.24.113.214:9000 \
          -Dsonar.login=d128d17268ae81a0b6b3d4d92f47cf7917af8126' */
        }
        }
      }
    }
  }
