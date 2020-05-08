pipeline {
  agent any
  parameters {
choice(name: 'CHOICE', choices: ['staging', 'production'], description: 'Pick something')

}

  stages {
    stage('Copy artifact') {
      steps {
        copyArtifacts filter: 'Assignment1', fingerprintArtifacts: true, projectName: 'Assignment1', selector: lastSuccessful()
      }
    }
    stage('Deliver') {
      steps {
        ansiblePlaybook credentialsId: 'toolbox-vagrant-key', inventory: "inventories/${params.CHOICE}/hosts.ini", playbook: 'playbook.yml', disableHostKeyChecking: true
      }
    }
  }
}
