pipeline {
    agent any
    environment {
        ANSIBLE_FORCE_COLOR = 'true'
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

        stage('Run Ansible Playbook') {
            steps {
                sshagent(['ansible-ssh-key']) {
                    sh 'ansible-playbook -i hosts.ini deploy.yml || exit 1'
                }
            }
        }
    }
}
