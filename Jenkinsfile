pipeline {
  agent { node { label 'dcs-jenkins_72_host2' } }
  environment {
    TEMP_VAR = 'true'
  }
  stages {
    stage('Hello') {
      steps {
        echo "hello from Jenkinsfile"
      }
    }
    stage('Checkout branch') {
      steps {
        // git branch: 'test', credentialsId: 'Project1TestPoll-2', url: 'https://github.com/jamesguise/publicTest.git'
        // checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'Project1TestPoll-2', url: 'https://github.com/jamesguise/publicTest.git']]])
        
        //git fetch origin +refs/pull/*/merge:refs/remotes/origin/pr/*
        //git fetch origin
        
        // checkout([$class: 'GitSCM', branches: [[name: "FETCH_HEAD"]],
          // extensions: [[$class: 'LocalBranch']],
          // userRemoteConfigs: [[refspec: "+refs/pull/${params.PR_NUMBER}/head:refs/remotes/origin/PR-${params.PR_NUMBER}", url: "https://${GITHUB_TOKEN}@github.com/${YOUR_REPO}"]]])
        
        // checkout([$class: 'GitSCM', branches: [[name: "FETCH_HEAD"]],
        
        checkout([$class: 'GitSCM', branches: [[name: '*/main']],
          extensions: [[$class: 'LocalBranch']],
          userRemoteConfigs: [[refspec: "+refs/pull/45/head:refs/remotes/origin/PR-45", credentialsId: 'Project1TestPoll-2', url: "https://github.com/jamesguise/publicTest.git"]]])
        
        // checkout([$class: 'GitSCM', branches: [[name: "FETCH_HEAD"]],
          // extensions: [[$class: 'LocalBranch']],
          // userRemoteConfigs: [[refspec: "+refs/pull/*/head:refs/remotes/origin/pr/*", credentialsId: 'Project1TestPoll-2', url: "https://github.com/jamesguise/publicTest.git"]]])
        
        //checkout scm
        echo "Checked out!"
      }
    }
    stage('Comment') {
      steps {
        script {
          if (env.CHANGE_ID) {
            echo 'FOUND A PR!!!'
            echo "CHANGE_ID: ${env.CHANGE_ID}"
            echo "CHANGE_TARGET: ${env.CHANGE_TARGET}"
            echo "CHANGE_URL: ${env.CHANGE_URL}"
            echo "CHANGE_TITLE: ${env.CHANGE_TITLE}"
            echo "CHANGE_AUTHOR: ${env.CHANGE_AUTHOR}"
            echo "BRANCH_NAME: ${env.BRANCH_NAME}"
            echo "CHANGE_BRANCH: ${env.CHANGE_BRANCH}"
            echo "BUILD_NUMBER: ${env.BUILD_NUMBER}"
            echo "BUILD_ID: ${env.BUILD_ID}"
            //echo "Pull Request ID: ${pullRequest.id}"
            //for (comment in pullRequest.comments) {
              //if (comment.user == "automation-user") {
                //pullRequest.deleteComment(comment.id)
              //}
            //}
            //def date = sh(returnStdout: true, script: "date -u").trim()
            //pullRequest.comment("Build ${env.BUILD_ID} ran at ${date}")
          }
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
      when {
        allOf {
          expression { env.CHANGE_ID != null }
          expression { env.CHANGE_TARGET != null }
        }
      }
      steps {
        echo "Building PR #${env.CHANGE_ID}"
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
