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
        // checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'Project1TestPoll-2', url: 'https://github.com/jamesguise/publicTest.git']]])
        // git fetch origin +refs/pull/*/merge:refs/remotes/origin/pr/*
        // checkout([$class: 'GitSCM', branches: [[name: "FETCH_HEAD"]],
          // extensions: [[$class: 'LocalBranch']],
          // userRemoteConfigs: [[refspec: "+refs/pull/${params.PR_NUMBER}/head:refs/remotes/origin/PR-${params.PR_NUMBER}", url: "https://${GITHUB_TOKEN}@github.com/${YOUR_REPO}"]]])
        // checkout([$class: 'GitSCM', branches: [[name: "FETCH_HEAD"]],
          // extensions: [[$class: 'LocalBranch']],
          // userRemoteConfigs: [[refspec: "+refs/pull/41/head:refs/remotes/origin/PR-41", credentialsId: 'Project1TestPoll-2', url: "https://github.com/jamesguise/publicTest.git"]]])
        checkout([$class: 'GitSCM', branches: [[name: "FETCH_HEAD"]],
          extensions: [[$class: 'LocalBranch']],
          userRemoteConfigs: [[refspec: "+refs/pull/*/head:refs/remotes/origin/pr/*", credentialsId: 'Project1TestPoll-2', url: "https://github.com/jamesguise/publicTest.git"]]])
        }
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
