def gv

pipeline {
  agent any
  environment{
    NEW_VERSION = '1.2.1'
    SERVER_CREDENTIALS = credentials('my-demo-pipeline')
  }
  parameters{
    // string(name:'VERSION', defaultValue:'',description:'version to deploy on prod')
    choice(name:'VERSION',choices:['1.2.1', '1.2.9'],description:'')
    booleanParam(name:'executeTests',defaultValue:true,description:'')
  }
  stages {
    stage("init"){
      steps{
        script{
          gv = load "script.groovy"  
        }
      }
    }
    stage("build"){
      when{
        expression{
          params.executeTests
        }
      }
      steps{
        script{
          gv.buildApp()
        }
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
        // withCredentials([
        //   usernamePassword(credentials:'my-demo-pipeline',usernameVariable: USER, passwordVariable: PWD)
        // ]){
        //   echo "some script ${USER} ${PWD}"
        // }
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
