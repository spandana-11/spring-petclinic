pipeline {
  agent any

  tools {
    maven 'MAVEN3'       // Configure this in Jenkins → Global Tool Config
    jdk 'JAVA17'         // Configure Java 17 here too
  }

  environment {
    SONARQUBE = 'SonarQubeServer'   // Jenkins → Manage → Configure SonarQube
  }

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/spring-projects/spring-petclinic.git'
      }
    }

    stage('Build') {
      steps {
        sh 'mvn clean install'
      }
    }

    stage('SonarQube Analysis') {
      steps {
        withSonarQubeEnv("${SONARQUBE}") {
          sh 'mvn sonar:sonar'
        }
      }
    }

    stage('Quality Gate') {
      steps {
        timeout(time: 2, unit: 'MINUTES') {
          waitForQualityGate abortPipeline: true
        }
      }
    }

    stage('Notify') {
      steps {
        echo "Send email/slack here"
        // mail to: 'you@example.com', subject: 'Build Finished', body: 'Success or failure'
      }
    }
  }
}
