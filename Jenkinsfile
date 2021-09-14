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
        git branch: 'main', credentialsId: 'Project1TestPoll-2', url: 'https://github.com/jamesguise/publicTest.git'
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
}
