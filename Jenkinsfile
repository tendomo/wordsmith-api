pipeline {
    agent any
    tools {
        maven 'Maven'
        git 'Default'
    }   
    stages {
        
        stage('Maven Build') {
            steps {
                sh 'mvn clean install'
                
            }
        }
        stage('Build Docker image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                 
                  sh 'docker login -u $USERNAME -p $PASSWORD'
    // Your Docker commands using the environment variables
                    
                  // Access JAR file path dynamically (if environment variable not set)
                   //jarFilePath = 'target/*.jar'   
                   // def pomFile = readMavenPom project: '.'
                    //def appName = pomFile.getName()
                  
                  sh "docker build -t word-api:latest -f Dockerfile ."
                
                 //sh 'docker build -t wordapi:${BUILD_NUMBER} .'
                  sh 'docker tag word-api:latest tendomo/word-api:${BUILD_NUMBER}'
                  sh 'docker push tendomo/word-api:${BUILD_NUMBER}'
                     
                     
                }
            }     
        }
    }
}
