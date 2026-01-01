pipeline {
    agent any
    tools {
        jdk 'jdk-21' // Ensure JDK is configured in Jenkins global tools
        maven 'maven-3.9.9' // Ensure Maven is configured in Jenkins global tools
    }

    // environment {
    //     NEXUS_VERSION='nexus3',
    //     NEXUS_PROTOCOL='http',
    //     NEXUS_URL='http://192.168.56.17:8081',
    //     NEXUS_REPO='vprofile-release',
    //     NEXUS_REPO_ID='vprofile-release',
    //     NEXUS_CREDENTIAL_ID='nexuslogin',
    //     ARTVERSION=${env.BUILD_ID}
    // }

    stages {
        stage('Fetch Code') {
            steps {
                git branch: 'atom', url: 'https://github.com/hkhcoder/vprofile-project.git'
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

        stage('Unit Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Checkstyle Analysis') {
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
        }


    }
}