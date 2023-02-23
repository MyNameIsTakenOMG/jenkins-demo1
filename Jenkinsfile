pipeline {
  agent any
  environment{
    NEW_VERSION = '1.2.1'
    SERVER_CREDENTIALS = credentials('server-user')
  }
  stages {
    stage("build"){
      steps{
        echo 'building application...'
        echo "building application ${NEW_VERSION}"
        nodejs('Node'){
          sh 'yarn install'
        }
      }
    }
    stage("test"){
      when {
        expression{
          BRANCH_NAME == 'main'
        }
      }
      steps{
        echo 'testing application...'
      }
    }
    stage("deploy"){
      steps{
        echo 'deploying application...'
        withCredentials([
          usernamePassword(credentials:'server-user',usernameVariable: USER, passwordVariable: PWD)
        ]){
          sh "some script ${USER} ${PWD}"
        }
      }
    }
  }
  post {
    always{
    }
    success{
    }
    failure{
    }
  }
}
