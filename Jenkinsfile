pipeline {
  agent any
  environment{
    NEW_VERSION = '1.2.1'
    SERVER_CREDENTIALS = credentials('server-user')
  }
  parameters{
    // string(name:'VERSION', defaultValue:'',description:'version to deploy on prod')
    choice(name:'VERSION',choices:['1.2.1', '1.2.9'],description:'')
    booleanParam(name:'executeTests',defaultValue:true,description:'')
  }
  stages {
    stage("build"){
      when{
        expression{
          params.executeTests
        }
      }
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
  // post {
  //   always{
  //   }
  //   success{
  //   }
  //   failure{
  //   }
  // }
}
