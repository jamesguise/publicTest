pipeline {
  agent { 
    node { 
      label 'dcs-jenkins_72_host2'
    } 
  }
  environment {
    TEMP_NUM = 5
    TEMP_CHANGED = "${sh('git diff --name-only ${GIT_PREVIOUS_COMMIT} ${GIT_COMMIT}')}"
  }
  stages {
    stage('Jenkins - Stage 0: Pre-Setup') {
      
      steps {
        echo "TEMP_NUM=${TEMP_NUM}"
        
        //sh 'git diff --name-only ${GIT_PREVIOUS_COMMIT} ${GIT_COMMIT}'
        echo "TEMP_CHANGED=${TEMP_CHANGED}"
        
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 1: Build csi-driver', status: 'QUEUED', summary: 'Building csi-driver', text: 'need to build csi-driver', title: 'Building csi-driver'
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 2: Build k8s files', status: 'QUEUED', summary: 'Building k8s files', text: 'need to build k8s files', title: 'Building k8s files'
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 3: Test csi-driver', status: 'QUEUED', summary: 'Testing csi-driver', text: 'need to test csi-driver', title: 'Testing csi-driver'
        sh 'env | sort'
      
        
      }
    }
    stage('Jenkins - Stage 1: Build csi-driver') {
      steps {
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 1: Build csi-driver', status: 'IN_PROGRESS', summary: 'Building csi-driver', text: 'need to build csi-driver', title: 'Building csi-driver'

        echo "Building csi-driver . . ."
        //build job: 'job-build3', parameters: [string(name: 'PR_NUMBER', value: "${env.CHANGE_ID}")]
        echo "Built csi-driver!"
        
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
  }
}
