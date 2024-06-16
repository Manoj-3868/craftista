pipeline {
  agent any
  tools {
    maven '3.9.6'
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
