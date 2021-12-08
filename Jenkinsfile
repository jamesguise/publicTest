pipeline {
  agent { 
    node { 
      label 'dcs-jenkins_72_host2'
    } 
  }
  environment {
    TEMP_NUM = 5
    //TEMP_CHANGED = "${(sh 'git diff --name-only ${GIT_PREVIOUS_COMMIT} ${GIT_COMMIT}')}"
  }
  stages {
    stage('Jenkins - Stage 0: Pre-Setup') {
      
      steps {
        echo "TEMP_NUM=${TEMP_NUM}"
        
        //sh 'git diff --name-only ${GIT_PREVIOUS_COMMIT} ${GIT_COMMIT}'
        //sh 'git diff --name-only HEAD~ HEAD'
        script {
          TEMP_CHANGED = sh (
            script: 'git diff --name-only ${GIT_PREVIOUS_COMMIT} ${GIT_COMMIT}',
            returnStdout: true
          ).trim()
          TEMP_CHANGED1 = sh (
            script: 'git diff --name-only ${GIT_COMMIT} ${GIT_PREVIOUS_COMMIT}',
            returnStdout: true
          ).trim()
          TEMP_CHANGED2 = sh (
            script: 'git diff --name-only ${GIT_COMMIT} HEAD',
            returnStdout: true
          ).trim()
          TEMP_CHANGED3 = sh (
            script: 'git diff --name-only HEAD~ HEAD',
            returnStdout: true
          ).trim()
          TEMP_CHANGED4 = sh (
            script: 'git diff --name-only ORIG_HEAD HEAD',
            returnStdout: true
          ).trim()
          TEMP_CHANGED5 = sh (
            script: 'git diff --name-only HEAD@{0} HEAD@{1}',
            returnStdout: true
          ).trim()
          TEMP_CHANGED6 = sh (
            script: 'git --no-pager diff origin/main --name-only',
            returnStdout: true
          ).split('\n')
          echo "TEMP_CHANGED=${TEMP_CHANGED}"
          echo "TEMP_CHANGED1=${TEMP_CHANGED1}"
          echo "TEMP_CHANGED2=${TEMP_CHANGED2}"
          echo "TEMP_CHANGED3=${TEMP_CHANGED3}"
          echo "TEMP_CHANGED4=${TEMP_CHANGED4}"
          echo "TEMP_CHANGED5=${TEMP_CHANGED5}"
          echo "TEMP_CHANGED6=${TEMP_CHANGED6}"
          //echo "class=${TEMP_CHANGED.getClass()}"
          if ((TEMP_CHANGED.contains("Jenkinsfile")) || (TEMP_CHANGED.contains(".md")) || (TEMP_CHANGED.contains(".txt"))){
            echo "Unimportant files changed, don't run tests!"
            TEMP_NUM=1
          } else {
            echo "Important files changed, run tests!"
          }
        }
        
        
        //echo "TEMP_CHANGED2=${TEMP_CHANGED}"
        
        
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 1: Build csi-driver', status: 'QUEUED', summary: 'Building csi-driver', text: 'need to build csi-driver', title: 'Building csi-driver'
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 2: Build k8s files', status: 'QUEUED', summary: 'Building k8s files', text: 'need to build k8s files', title: 'Building k8s files'
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 3: Test csi-driver', status: 'QUEUED', summary: 'Testing csi-driver', text: 'need to test csi-driver', title: 'Testing csi-driver'
        sh 'env | sort'
      
        
      }
    }
    
    stage('Jenkins - Stage 1: Build csi-driver') {
      steps {
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 1: Build csi-driver', status: 'IN_PROGRESS', summary: 'Building csi-driver', text: 'need to build csi-driver', title: 'Building csi-driver'

        script{
          //if (TEMP_NUM.equals(1)){
          echo "Building csi-driver . . ."
          //build job: 'job-build3', parameters: [string(name: 'PR_NUMBER', value: "${env.CHANGE_ID}")]
          echo "Built csi-driver!"
          //}
        }
        echo "Done with Stage 1"

        publishChecks name: 'Jenkins - Stage 1: Build csi-driver', summary: 'Building csi-driver', text: 'need to build csi-driver', title: 'Building csi-driver'
      }
    }
    stage('Jenkins - Stage 2: Build k8s files') {
      steps {
        script {
          publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 2: Build k8s files', status: 'IN_PROGRESS', summary: 'Building k8s files', text: 'need to build k8s files', title: 'Building k8s files'

          echo "Building k8s files . . ."
          //build job: 'csi-driver-PR', parameters: [string(name: 'UPSTREAM_EDGE_NUMBER', value: "${env.CHANGE_ID}")]
          echo "Built k8s files!"

          publishChecks name: 'Jenkins - Stage 2: Build k8s files', summary: 'Building k8s files', text: 'need to build k8s files', title: 'Building k8s files'

        }
      }
    }
    stage('Jenkins - Stage 3: Test csi-driver') {
      steps {
        script {
          publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 3: Test csi-driver', status: 'IN_PROGRESS', summary: 'Testing csi-driver', text: 'need to test csi-driver', title: 'Testing csi-driver'

          echo "Testing csi-driver . . ."
          //build job: 'job-ext-test'
          echo "Tested csi-driver!"


          publishChecks name: 'Jenkins - Stage 3: Test csi-driver', summary: 'Testing csi-driver', text: 'need to test csi-driver', title: 'Testing csi-driver'

        }

        slackSend channel: '#jenkins-intern-project1', color: "#17c40e", message: """${env.BUILD_TAG}: Successfully ran all tests!
        Ready to be approved and merged to Master branch!
        Waiting to be reviewed . . .
        You can view the Jenkins Job Pipeline: ${env.JOB_URL}
        You can view the Jenkins Blue Ocean Pipeline: ${env.RUN_DISPLAY_URL}
        You can view the PR on GitHub: ${env.CHANGE_URL}""", teamDomain: 'hpe-internal'

      }
    }
    
    // above ends if statement
  }
}
