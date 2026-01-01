pipeline {
    agent any
    tools {
        jdk 'jdk-21' // Ensure JDK is configured in Jenkins global tools
        maven 'maven-3.9.9' // Ensure Maven is configured in Jenkins global tools
    }

    environment {}
    stages {
        stage('Fetch Code') {
            steps {
                git branch: 'atom', url: 'https://github.com/hkhcoder/vprofile-project.git'
            }
        }

        stage('Unit Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn install -DskipTests'
            }
            post {
                success {
                    echo 'Archiving the build artifacts...'
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
    }
}