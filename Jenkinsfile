pipeline {
    agent any

    triggers {
        // Not strictly needed with webhook, but useful for scheduled re-indexing
        // pollSCM('H/5 * * * *') 
    }

    stages {
        stage('Checkout') {
            steps {
                // Checks out the code from the branch or merged PR.
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Replace with build commands for your stack
                sh 'echo "Building project..."'
            }
        }

        stage('Test') {
            steps {
                // Replace with test commands
                sh 'echo "Running tests..."'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Assumes Dockerfile present at the repo root
                    def imageName = "myorg/myapp:${env.BUILD_NUMBER}"
                    sh "docker build -t ${imageName} ."
                    // Optionally:
                    // withCredentials([string(credentialsId: 'DOCKERHUB_TOKEN', variable: 'TOKEN')]) {
                    //   sh "docker login -u myusername -p $TOKEN"
                    //   sh "docker push ${imageName}"
                    // }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
