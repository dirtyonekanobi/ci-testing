pipeline {
  agent {
    dockerfile {
          filename 'Dockerfile'
          args '--user root'
          reuseNode true
    }
  }
  stages {
    stage('build') {
      steps {
        sh 'echo Teste'
      }
    }
    stage('test') {
      steps {
        script {
          try {
                githubNotify status: "PENDING", sha: "${GITHUB_PR_HEAD_SHA}", description: "Build started...", credentialsId: "ken_token1", account: "itdependsnetworks", repo: "ci-testing"
                sh 'printenv'
           } catch(err) {
                githubNotify status: "FAILURE",  sha: "${GITHUB_PR_HEAD_SHA}", description: "Build failed...", credentialsId: "ken_token1", account: "itdependsnetworks", repo: "ci-testing"
                throw err
           }
         }
       }
    }
    stage('run_commands') {
      steps {
        script {
          try {
                sh 'printenv'
           } catch(err) {
                githubNotify status: "FAILURE", sha: "${GITHUB_PR_HEAD_SHA}", description: "Build failed...", credentialsId: "ken_token1", account: "itdependsnetworks", repo: "ci-testing"
                throw err
           } finally {
                sh "echo 'shell scripts to deploy to server...'"
                githubNotify status: "SUCCESS", sha: "${GITHUB_PR_HEAD_SHA}", description: "Build completed...", credentialsId: "ken_token1", account: "itdependsnetworks", repo: "ci-testing"

           }
         }
       }
    }
  }
}
