
pipeline {
    agent any

    stages {

        stage('Get Source') {
            steps {
                git url: 'https://github.com/wender-firmino/pedelogo-catalogo.git', branch: 'dev1'
            }
        }
        stage('Docker Build Image') {
            steps {
                script {
                    dockerapp = docker.build("wender-firmino/api-produto:${env.BUILD_ID}",
                      '-f ./src/PedeLogo.Catalogo.Api/Dockerfile .')
                }
            }
        }
         stage('Docker Push Image') {
            steps {
                script {
                        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }
    }
}
