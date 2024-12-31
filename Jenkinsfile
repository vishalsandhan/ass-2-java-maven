pipeline {
    agent any
    tools {
        maven 'sonarmaven'
    }
    environment {
        SONAR_TOKEN = credentials('sonar-token')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build with Maven') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Run Automation Tests') {
            steps {
                script {
                    // Run your tests with Maven (e.g., unit tests with JUnit)
                    sh "${MAVEN_HOME}/bin/mvn test"
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                steps {
                withSonarQubeEnv('sonarqube') {
                    bat """
                    -Dsonar.projectKey=Ass-2-maven-project \
                    -Dsonar.projectName='Ass-2-maven-project' \
                    -Dsonar.host.url=http://localhost:9000 \
                    -Dsonar.host.url=http://localhost:9000 \
                    -Dsonar.token=$SONAR_TOKEN
                    """
                }
            }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
