pipeline {
    agent any 
    stages {
        stage('Compile and Clean') { 
            steps {

                sh "mvn clean compile"
            }
        }
       

        stage('deploy') { 
            steps {
                sh "mvn package"
            }
        }


        stage('Build Docker image'){
            steps {
              
                sh 'docker build -t  bichitra1994/docker_jenkins_springboot .'
            }
        }

        stage('Docker Login'){
            
            steps {
                 withCredentials([string(credentialsId: 'DockerId', variable: 'Dockerpwd')]) {
                    sh "docker login -u bichitra1994 -p ${Dockerpwd}"
                }
            }                
        }

        stage('Docker Push'){
            steps {
                sh 'docker push bichitra1994/docker_jenkins_springboot'
            }
        }
        
        stage('Docker deploy'){
            steps {
               
                sh 'docker run -itd -p  8081:8080 bichitra1994/docker_jenkins_springboot'
            }
        }

        
        stage('Archving') { 
            steps {
                 archiveArtifacts '**/target/*.jar'
            }
        }
    }
}
