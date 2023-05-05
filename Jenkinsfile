pipeline {
  agent any
    tools {
      maven 'mvn3'
                 jdk 'jdk11'
    }
    stages {      
        stage('Build maven ') {
            steps { 
                    sh 'pwd'      
                    sh 'mvn  clean install package'
            }
        }
        
        stage('Copy Artifact') {
           steps { 
                   sh 'pwd'
		   sh 'cp -r target/*.jar docker'
           }
        }
         
        stage('Build docker image') {
           steps {
               script {         
                 def customImage = docker.build('azuretushar2022/petclinic', "./docker")
                 docker.withRegistry('https://acrregistryabc.azurecr.io', 'acr_demo') {
                 customImage.push("${env.BUILD_NUMBER}")
                 }                     
           }
        }
	  }
    }
}
