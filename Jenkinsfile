pipeline {
    agent {
        label 'ansible-docker'
    }
    stages {
        stage('Source') {
            steps {
                git 'https://github.com/emiliogh/git_prueba.git'
            }
        }
        stage('Validar conexión ansible') {
            steps {
                echo "validar conexión ansible controlador con nodo"
				sshPublisher(publishers:
				[sshPublisherDesc(
				    configName:'AnsibleController',
					transfers: [
					    sshTransfer(
						cleanRemote:false,
						execCommand:'ansible-playbook playbook_ping.yml --limit nodo',
						execTimeout:120000
						)
					],
					usePromotionTimestamp: false,
					useWorkspaceInPromotion: false,
					verbose: false)
				])
            }
        }
    }
	options {
        skipDefaultCheckout(true)
    }
}
