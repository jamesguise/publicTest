pipeline {
  agent { 
    node { 
      label 'dcs-jenkins_72_host2'
    } 
  }
  environment {
    TEMP_NUM = 5
  }
  stages {
    stage('Jenkins - Stage 0: Pre-Setup') {
      steps {
        script {
          
          TEMP_CHANGED = sh (
            script: 'git --no-pager diff origin/${CHANGE_TARGET} --name-only',
            returnStdout: true
          ).split('\n')
          
          echo "TEMP_CHANGED=${TEMP_CHANGED}"
          
          if ((TEMP_CHANGED.contains("Jenkinsfile")) || (TEMP_CHANGED.contains(".go")) || (TEMP_CHANGED.contains(".sh")) || (TEMP_CHANGED.contains(".repo")) || (TEMP_CHANGED.contains(".service")) || 
              (TEMP_CHANGED.contains("Dockerfile")) || (TEMP_CHANGED.contains(".yaml")) || (TEMP_CHANGED.contains("Makefile")) || (TEMP_CHANGED.contains("Jenkinsfile")) || (TEMP_CHANGED.contains("COPYING")) || 
              (TEMP_CHANGED.contains("COMPATIBLE")) || (TEMP_CHANGED.contains(".proto")) || (TEMP_CHANGED.contains(".mod")) || (TEMP_CHANGED.contains(".sum"))){
            echo "Important files were changed, run tests!"
            TEMP_NUM=1
          } else {
            echo "No important files were changed, no need to run tests!"
          }
        }
        
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
          if (TEMP_NUM.equals(1)){
            echo "Building csi-driver . . ."
            build job: 'job-build3', parameters: [string(name: 'PR_NUMBER', value: "${env.CHANGE_ID}")]
            echo "Built csi-driver!"
          } else {
            echo "No important files were changed, skipping stage!"
          }
        }

        publishChecks name: 'Jenkins - Stage 1: Build csi-driver', summary: 'Building csi-driver', text: 'need to build csi-driver', title: 'Building csi-driver'
      }
    }
    stage('Jenkins - Stage 2: Build k8s files') {
      steps {
        script {
          publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 2: Build k8s files', status: 'IN_PROGRESS', summary: 'Building k8s files', text: 'need to build k8s files', title: 'Building k8s files'

          if (TEMP_NUM.equals(1)){
            echo "Building k8s files . . ."
            build job: 'csi-driver-PR', parameters: [string(name: 'UPSTREAM_EDGE_NUMBER', value: "${env.CHANGE_ID}")]
            echo "Built k8s files!"
          } else {
            echo "No important files were changed, skipping stage!"
          }

          publishChecks name: 'Jenkins - Stage 2: Build k8s files', summary: 'Building k8s files', text: 'need to build k8s files', title: 'Building k8s files'

        }
      }
    }
    stage('Jenkins - Stage 3: Test csi-driver') {
      steps {
        script {
          publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 3: Test csi-driver', status: 'IN_PROGRESS', summary: 'Testing csi-driver', text: 'need to test csi-driver', title: 'Testing csi-driver'

          if (TEMP_NUM.equals(1)){
            echo "Testing csi-driver . . ."
            build job: 'job-ext-test'
            echo "Tested csi-driver!"
          } else {
            echo "No important files were changed, skipping stage!"
          }

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
  }
}
