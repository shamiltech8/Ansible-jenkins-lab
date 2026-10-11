pipeline {
    agent any

    stages {
        stage('Check Tools') {
            steps {
                sh 'git --version'
                sh 'ansible-playbook --version'
            }
        }

        stage('Validate Playbook') {
            steps {
                sh 'ansible-playbook --syntax-check -i localhost, playbook.yml'
            }
        }

        stage('Run Ansible') {
            steps {
                sh 'ansible-playbook -i localhost, playbook.yml'
            }
        }
    }
}
