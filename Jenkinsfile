
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat 'mvn -B clean compile'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn -B test'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn -B package'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar',
                                 fingerprint: true
            }
        }

        stage('Deploy Locally') {
            steps {
                bat 'if not exist deploy mkdir deploy'
                bat 'copy /Y target\\devops-webapp-1.0-SNAPSHOT.jar deploy\\devops-webapp.jar'
                bat 'dir deploy'
            }
        }
    }

    post {
        success {
            echo 'CI/CD pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
