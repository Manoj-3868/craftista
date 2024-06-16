pipeline {
  agent any
  stages {
    stage('Build voting') {
      steps {
        echo 'building voting app'
        dir(path: 'voting') {
          sh 'mvn compile'
        }

      }
    }

    stage('Test voting') {
      steps {
        dir(path: 'voting') {
          sh 'mvn clean test'
        }

      }
    }

    stage('Package voting') {
      steps {
        dir(path: 'voting') {
          sh 'mvn package -DskipTests'
        }

        archiveArtifacts '**/target/*.jar'
      }
    }

  }
  tools {
    maven 'Maven 3.9.6'
  }
  post {
    always {
      echo 'complited craftia application'
    }

  }
}