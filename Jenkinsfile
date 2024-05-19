pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'mvn clean package'
            }
        }

        stage('Unit Testing') {
            steps {
                echo 'Running unit tests...'
                sh 'mvn test'
            }
        }

        stage('Static Code Analysis') {
            steps {
                echo 'Performing static code analysis...'
                sh 'mvn sonar:sonar'
            }
        }

        stage('SAST') {
            steps {
                echo 'Running SAST...'
                // Example command, adjust according to your SAST tool
                sh 'sast-command'
            }
        }

        stage('DAST') {
            steps {
                echo 'Running DAST...'
                // Example command, adjust according to your DAST tool
                sh 'dast-command'
            }
        }

        stage('Docker Image Creation') {
            steps {
                echo 'Creating Docker image...'
                dockerImage = docker.build("my-java-app:${env.BUILD_NUMBER}")
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                echo 'Deploying to Kubernetes...'
                script {
                    // Use Argo CD plugin to sync the application
                    argocdAppSync('my-java-app', 'staging')
                }
            }
        }
    }
}
