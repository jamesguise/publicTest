pipeline {
  agent { node { label 'dcs-jenkins_72_host2' } }
  stages {
    stage('Hello') {
      steps {
        echo "hello from Jenkinsfile"
      }
    }
    stage('Checkout branch') {
      steps {
        // git branch: 'main', credentialsId: 'Project1TestPoll-2', url: 'https://github.com/jamesguise/publicTest.git'
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'Project1TestPoll-2', url: 'https://github.com/jamesguise/publicTest.git']]])
        git fetch origin +refs/pull/*/merge:refs/remotes/origin/pr/*      
      }
    }
    stage('Try a Job') {
      steps {
        build job: 'GdummyTest'
      }
    }
    stage('Try a MultiJob') {
      steps {
        build job: 'MultiJob-Guise-test'
        echo "MultiJob done"
      }
    }
    stage('Get PR info') {
      steps {
        echo env.CHANGE_ID
      }
    }
  }
  post {
    always {
      echo "Test run completed"
    }
    success {
      echo "Successfully!"
    }
    failure {
      echo "Failed!"
    }
    unstable {
      echo "The run was marked as unstable!"
    }
  }
}
