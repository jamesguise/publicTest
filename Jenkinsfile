pipeline {
  agent { 
    node { 
      label 'dcs-jenkins_72_host2'
    } 
  }
  environment {
    TEMP_VAR = 'true'
  }
  stages {
    stage('Check PR Queue') {
      steps {
        publishChecks(name: 'Check PR Queue', status: 'in_progress', summary: 'Checking...')

        //withCredentials([gitUsernamePassword(credentialsId: 'Project1TestPoll-2', gitToolName: 'Default')]) {
          // some block
          //sh '''
          //curl "https://api.github.com/repos/jamesguise/publicTest/statuses/$GIT_COMMIT?access_token=Project1TestPoll-2" \
          //  -H "Content-Type: application/json" \
          //  -X POST \
          //  -d "{\"state\": \"success\",\"context\": \"continuous-integration/jenkins\", \"description\": \"Jenkins\", \"target_url\": ${env.JENKINS_URL}/job/${env.JOB_NAME}/$BUILD_NUMBER/console\"}"
          
          
          //curl -H "Content-Type: application/json" \
          //     -H "Accept: application/vnd.github.antiope-preview+json" \
          //     -H "authorization: Bearer ${Project1TestPoll-2}" \
          //     -d '{"name": "check_run", \
          //          "head_sha": "'${GIT_COMMIT}'", \
          //          "status": "in_progress", \
          //          "external_id": "42", \
          //          "started_at": "2020-03-05T11:14:52Z", \
          //          "output": {"title": "Check run from Jenkins!", \
          //                     "summary": "This is a check which has been generated from Jenkins as Github App", \
          //                     "text": ". . . and that is awesome"}}' https://api.github.com/repos/<org>/<repo>/check-runs
          //'''
        //}
       
        sh 'env | sort'
        //echo "branch: ${d.GIT_BRANCH}"
        //echo "commit: ${d.GIT_COMMIT}"
        //sh("git fetch origin pull/46/head:origin/PR-46")
        //sh "git checkout origin/prTestdummy"
        
        //checkout([$class: 'GitSCM', branches: [[name: "'*/main'"]],
          //extensions: [[$class: 'LocalBranch']],
          //userRemoteConfigs: [[refspec: "+refs/pull/*/head:refs/remotes/origin/pr/*", credentialsId: 'Project1TestPoll-2', url: "https://github.com/jamesguise/publicTest.git"]]])
        
        echo "Check PR Queue . . ."
        
        echo "CHANGE_ID: ${env.CHANGE_ID}"
        echo "CHANGE_TARGET: ${env.CHANGE_TARGET}"
        echo "CHANGE_URL: ${env.CHANGE_URL}"
        echo "CHANGE_TITLE: ${env.CHANGE_TITLE}"
        echo "CHANGE_AUTHOR: ${env.CHANGE_AUTHOR}"
        echo "BRANCH_NAME: ${env.BRANCH_NAME}"
        echo "CHANGE_BRANCH: ${env.CHANGE_BRANCH}"
        echo "BUILD_NUMBER: ${env.BUILD_NUMBER}"
        echo "BUILD_ID: ${env.BUILD_ID}"
        echo "NODE_NAME: ${env.NODE_NAME}"
        echo "JENKINS_URL: ${env.JENKINS_URL}"
        echo "JENKINS_HOME: ${env.JENKINS_HOME}"
        echo "JOB_NAME: ${env.JOB_NAME}"
      }
    }
    stage('Checkout PR/branch') {
      steps {
        publishChecks(name: 'Checkout PR', status: 'in_progress', summary: 'Checking out PR...')
        //checkout([$class: 'GitSCM',
          //        branches: [[name: '*/main']],
            //      extensions: [],
              //    userRemoteConfigs: [[refspec: "+refs/pull/*:refs/remotes/origin/pr/*", credentialsId: 'Project1TestPoll-2', url: "https://github.com/jamesguise/publicTest.git"]]])
        // echo scm.getUserRemoteConfigs()
        // git branch: 'test', credentialsId: 'Project1TestPoll-2', url: 'https://github.com/jamesguise/publicTest.git'
        // checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'Project1TestPoll-2', url: 'https://github.com/jamesguise/publicTest.git']]])
        //echo "CHANGE_ID: ${env.CHANGE_ID}"
        //git fetch origin +refs/pull/*/merge:refs/remotes/origin/pr/*
        //git fetch origin
        
        // checkout([$class: 'GitSCM', branches: [[name: "FETCH_HEAD"]],
          // extensions: [[$class: 'LocalBranch']],
          // userRemoteConfigs: [[refspec: "+refs/pull/${params.PR_NUMBER}/head:refs/remotes/origin/PR-${params.PR_NUMBER}", url: "https://${GITHUB_TOKEN}@github.com/${YOUR_REPO}"]]])
        
        // checkout([$class: 'GitSCM', branches: [[name: "FETCH_HEAD"]],
        
        //checkout([$class: 'GitSCM', branches: [[name: '*/main']],
          //extensions: [[$class: 'LocalBranch']],
          //userRemoteConfigs: [[refspec: "+refs/pull/46/head:refs/remotes/origin/PR-46", credentialsId: 'Project1TestPoll-2', url: "https://github.com/jamesguise/publicTest.git"]]])
        
        // checkout([$class: 'GitSCM', branches: [[name: "FETCH_HEAD"]],
          // extensions: [[$class: 'LocalBranch']],
          // userRemoteConfigs: [[refspec: "+refs/pull/*/head:refs/remotes/origin/pr/*", credentialsId: 'Project1TestPoll-2', url: "https://github.com/jamesguise/publicTest.git"]]])
        
        //checkout scm
        echo "Checked out a PR/branch!"
        echo "CHANGE_ID: ${env.CHANGE_ID}"
        // githubNotify account: 'jamesguise', context: '', credentialsId: 'Project1TestPoll-2', description: '', gitApiUrl: 'httms://api.github.com', repo: 'publicTest', sha: '37f572c', status: 'PENDING', targetUrl: ''
        //gitHubPRStatus githubPRMessage('${GITHUB_PR_COND_REF} run started')
      }
    }
    stage('Build csi-driver') {
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
            echo 'Build csi-driver . . .'
          }
        }
      }
    }
    stage('Run csi-driver tests') {
      steps {
        //build job: 'GdummyTest'
        echo 'Run csi-driver tests . . .'
      }
    }
    stage('Try a MultiJob') {
      steps {
        //build job: 'MultiJob-Guise-test'
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
}
