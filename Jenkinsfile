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
    stage('Integration Test') {
      agent{
	docker {
	image 'postman/newman'
	args '--entrypoint='
}} 
	steps {
	    sh 'newman run "https://www.getpostman.com/collections/e28663e6208d00ce79d5"'
		}
}
  }
}
