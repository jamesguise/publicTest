pipeline {
  agent { 
    node { 
      label 'dcs-jenkins_72_host2'
    } 
  }
  environment {
    TEMP_VAR = 'true'
    d = checkout scm
  }
  stages {
    stage('Hola!!') {
      steps {
        
        
        //checkout([$class: 'GitSCM', branches: [[name: "'*/main'"]],
          //extensions: [[$class: 'LocalBranch']],
          //userRemoteConfigs: [[refspec: "+refs/pull/*/head:refs/remotes/origin/pr/*", credentialsId: 'Project1TestPoll-2', url: "https://github.com/jamesguise/publicTest.git"]]])
        
        echo "Hola from master Jenkinsfile"
        // echo "CHANGE_ID: ${env.BITBUCKET_PULL_REQUEST_ID}"
      }
    }
  }
}
