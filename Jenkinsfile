pipeline {
    agent any
    environment {
        VERSION = "${env.BUILD_ID}"
    }
    stages {
        stage('mvn clean') {
            agent {
                docker {
                    image 'maven'
                    args '-v $HOME/.m2:/root/.m2'
                }
            }
            steps {
                sh "mvn clean install"
            }
        }
        stage('push') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'docker_pass', variable: 'docker')]) {
                        sh '''
                        docker build . -t msaqib934/devops-training:${VERSION}
                        docker push msaqib934/devops-training:${VERSION}
                        docker rmi msaqib934/devops-training:${VERSION}
                        '''
                    }
                }
            }
        }
    }
}
