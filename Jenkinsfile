pipeline {
  agent none
  stages {
    stage('Build voting') {
      agent {
        docker {
          image 'maven:3.9.6-eclipse-temurin-17-alpine'
        }

      }
      steps {
        echo 'building voting app'
        dir(path: 'voting') {
          sh 'mvn compile'
        }

      }
    }

    stage('Test voting') {
      agent {
        docker {
          image 'maven:3.9.6-eclipse-temurin-17-alpine'
        }

      }
      steps {
        dir(path: 'voting') {
          sh 'mvn clean test'
        }

      }
    }

    stage('Package voting') {
      parallel {
        stage('Package voting') {
          agent {
            docker {
              image 'maven:3.9.6-eclipse-temurin-17-alpine'
            }
          
          }
           when {branch:'main'}
          steps {
            dir(path: 'voting') {
              sh 'mvn package -DskipTests'
            }

            archiveArtifacts '**/target/*.jar'
          }
        }

        stage('Docker B&P') {
          agent any
          when {branch:'main'}
          steps {
            script {
              docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
                def commitHash = env.GIT_COMMIT.take(7)
                def dockerImage = docker.build("manoj3868/craftista-voting:${commitHash}", "./voting")
                dockerImage.push()
                dockerImage.push("latest")
                dockerImage.push("dev")
              }
            }

          }
        }

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
