pipeline {
  agent any

  stages {
    stage('Copy artifact') {
      steps {
        copyArtifacts filter: 'Assignment1', fingerprintArtifacts: true, projectName: 'Assignment1', selector: lastSuccessful()
      }
    }
    stage('Deliver') {
      steps {
        ansiblePlaybook credentialsId: 'toolbox-vagrant-key', inventory: 'hosts.ini', playbook: 'playbook.yml', disableHostKeyChecking: true
      }
    }
  }
}
