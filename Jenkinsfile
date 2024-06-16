pipeline {
  agent any
  tools {
    maven 'Maven 3.9.6'
  }
  stages{
    stage('voting application'){
        steps{
          echo 'building voting app'
          dir('voting'){
            sh 'mvn compile'
          }
        }      
    }
  }
  post{
    always{
      echo 'complited craftia application'
    }
  }
}
