pipeline {
    agent {
        node { label 'jenkinsworker00' }
    }
    
    environment {
        HARBOR_CREDENTIALS = 'harbor-jenkins-ci-credentials'
        FPM_IMAGE_NAME = 'jenkins-ci/fpm'
        GO_IMAGE_NAME = 'jenkins-ci/go1.21.0'
        SANITIZED_BRANCH_NAME = env.BRANCH_NAME.replace('/', '_')
    }
    
    stages {
        stage('Build and push fpm Image') {
            steps {
                script {
                    docker.withRegistry('https://harbor.cloud.infn.it', HARBOR_CREDENTIALS) {
                        docker.build("${FPM_IMAGE_NAME}:${env.SANITIZED_BRANCH_NAME}", "-f golang/Dockerfile fpm").push()
                    }

                    
                }
            }
        }
        stage('Build and push go 1.21.0 Image') {
            steps {
                script {
                    docker.withRegistry('https://harbor.cloud.infn.it', HARBOR_CREDENTIALS) {
                        docker.build("${GO_IMAGE_NAME}:${env.SANITIZED_BRANCH_NAME}", "-f golang/Dockerfile fpm").push()
                    }   
                }
            }
        }
    }
    post {
        success {
            echo 'Docker images build and push successful!'
        }
        failure {
            echo 'Docker images build and push failed!'
            // Optionally, you can add a notification or other failure-handling logic here.
        }
    }
}
