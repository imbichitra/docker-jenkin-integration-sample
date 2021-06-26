pipeline {
    agent any 
    stages {
        stage('Compile and Clean') { 
            steps {

                bat "mvn clean compile"
            }
        }
       

        stage('deploy') { 
            steps {
                bat "mvn package"
            }
        }


        stage('Build Docker image'){
            steps {
              
                bat 'docker build -t  bichitra1994/docker_jenkins_springboot'
            }
        }

        stage('Docker Login'){
            
            steps {
                 withCredentials([string(credentialsId: 'DockerId', variable: 'Dockerpwd')]) {
                    bat "docker login -u bichitra1994 -p ${Dockerpwd}"
                }
            }                
        }

        stage('Docker Push'){
            steps {
                bat 'docker push bichitra1994/docker_jenkins_springboot'
            }
        }
        
        stage('Docker deploy'){
            steps {
               
                bat 'docker run -itd -p  8081:9090 bichitra1994/docker_jenkins_springboot'
            }
        }

        
        stage('Archving') { 
            steps {
                 archiveArtifacts '**/target/*.jar'
            }
        }
    }
}
