pipeline{
    agent any
    
   environment{
     PATH = "/opt/maven3/bin:$PATH"
    }
    stages{
        stage("Git Checkout"){
            steps{
           git credentialsId: 'babuNagendra9848', url: 'https://github.com/babuNagendra9848/hello-world.git'
            }
        }
        stage("Maven Build"){
            steps{
                sh "mvn clean package"
            
            }
        }
        stage("deploy-dev"){
            steps{
                sshagent(['tomcat-new']) {
                sh """
                    scp -o StrictHostKeyChecking=no target/myweb.war  ec2-user@3.86.25.106:/home/ec2-user/apache-tomcat-10.1.10/webapps/
                    
                    ssh ec2-user@3.86.25.106 /home/ec2-user/apache-tomcat-10.1.10/bin/shutdown.sh
                    
                    ssh ec2-user@3.86.25.106 /home/ec2-user/apache-tomcat-10.1.10/bin/startup.sh
                
                """
            }
            
            }
        }
    }
}
