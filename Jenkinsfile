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

        stage('Run Local Ansible') {
            steps {
                sh 'ansible-playbook -i localhost, playbook.yml'
            }
        }

    stage('Inspect EC2 Server') {
        steps {
            sshagent(credentials: ['ec2-ansible-ssh']) {
                sh '''
                    export ANSIBLE_HOST_KEY_CHECKING=False

                    ansible all -i '15.206.66.123,' \
                        -u ubuntu -m command -a 'hostname'

                    ansible all -i '15.206.66.123,' \
                        -u ubuntu -m command -a 'uname -srm'
                '''
            }
        }
    }
