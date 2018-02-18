pipeline {
    agent any

    stages {
        def mvnHome
        stage('Prepare') { // for display purposes
            // Get the Maven tool.
            // ** NOTE: This 'M3' Maven tool must be configured
            // **       in the global configuration.
            mvnHome = tool 'M3'
        }
        stage('Build') {
            steps {
                echo 'Building..'
                if (isUnix()) {
                    sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
                } else {
                    bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
        stage('Results') {
            junit '**/target/surefire-reports/TEST-*.xml'
            archive 'target/*.jar'
        }
    }
}