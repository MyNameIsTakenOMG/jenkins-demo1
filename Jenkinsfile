pipeline {
  agent any
  stages {
    stage("build"){
      steps{
        echo 'building application...'
        nodejs('node'){
          sh 'yarn install'
        }
      }
    }
    stage("test"){
      steps{
        echo 'testing application...'
      }
    }
    stage("deploy"){
      steps{
        echo 'deploying application...'
      }
    }
  }
}
