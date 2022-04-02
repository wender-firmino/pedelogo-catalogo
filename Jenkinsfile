pipeline {
    
    environment {
        registry = "wfirmino@gmail.com/api-produto"
        registryCredential = 'dockerhub_id'
        dockerImage = ''
    }
    
    agent any

    stages {

        stage('Get Source') {
            steps {
                git url: 'https://github.com/wender-firmino/pedelogo-catalogo.git', branch: 'dev1'
            }
        }
       
        stage('Building our image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Deploy our image') {
            steps{
                script 
                {
                    docker.withRegistry( '', registryCredential ) 
                    {
                        dockerImage.push()
                    }
                }
            }
        }
        
    }
}
