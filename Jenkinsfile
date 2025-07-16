pipeline {
    agent any

    environment {
        MAVEN_HOME = tool 'Maven' // Define Maven tool name as configured in Jenkins Global Tools
        SONARQUBE = 'SonarQube'   // Name you give your SonarQube server in Jenkins > Configure
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/spandana-11/spring-petclinic.git'
            }
        }

        stage('Build with Maven') {
            steps {
        sh "${MAVEN_HOME}/bin/mvn clean install"
    }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=petclinic -Dsonar.host.url=http://localhost:9000'
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}
