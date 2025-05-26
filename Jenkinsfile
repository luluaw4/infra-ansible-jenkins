pipeline {
    agent any
    environment {
        ANSIBLE_FORCE_COLOR = 'true'
        ANSIBLE_HOST_KEY_CHECKING = 'False'
    }
    stages {
        stage('Checkout Source') {
            steps {
                git branch: 'main', url: 'https://github.com/luluaw4/infra-ansible-jenkins.git'
            }
        }

        stage('Print Working Directory') {
            steps {
                sh 'pwd && ls -lah'
            }
        }

        stage('Validate Ansible Playbook') {
            steps {
                sh 'ansible-playbook --syntax-check -i host.ini deploy.yml'
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sshagent(['ansible-ssh-key']) {
                    sh 'ansible-playbook -i host.ini deploy.yml'
                }
            }
        }
    }
}
