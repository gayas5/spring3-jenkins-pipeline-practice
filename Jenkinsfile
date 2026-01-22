pipeline {
    agent any

    tools {
        maven 'maven-3'   // must match Jenkins tool name
    }

    environment {
        MAVEN_OPTS = "-Dmaven.repo.local=/var/jenkins_home/.m2/repository"
    }

    options {
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/gayas5/spring3-jenkins-pipeline-practice.git'
            }
        }

        stage('Maven Build') {
            steps {
                sh '''
                    mvn -B clean install \
                    -DskipTests \
                    -Dmaven.test.skip=true
                '''
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }
    }

    post {
        success {
            echo ' Build completed successfully'
        }
        failure {
            echo ' Build failed'
        }
    }
}
