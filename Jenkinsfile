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

        stage('Test EC2 Connection') {
            steps {
                sshagent(credentials: ['ec2-ansible-ssh']) {
                    sh '''

                        ansible all -i '15.206.66.123,' \
                            -u ubuntu -m ping
                    '''
                }
            }
        }

        stage('Inspect EC2 Server') {
            steps {
                sshagent(credentials: ['ec2-ansible-ssh']) {
                    sh '''

                        ansible all -i '15.206.66.123,' \
                            -u ubuntu -m command -a 'hostname'

                        ansible all -i '15.206.66.123,' \
                            -u ubuntu -m command -a 'uname -srm'
                    '''
                }
            }
        }
        
        
        stage('Verify Docker Nginx on EC2') {
            steps {
                sshagent(credentials: ['ec2-ansible-ssh']) {
                    sh '''

                        ansible-playbook \
                            -i '15.206.66.123,' \
                            -u ubuntu \
                            ec2-playbook.yml
                    '''
                }
            }
        }


        stage('Configure EC2 with Ansible') {
            steps {
                sshagent(credentials: ['ec2-ansible-ssh']) {
                    sh '''
                        ansible-playbook \
                            -i '15.206.66.123,' \
                            -u ubuntu \
                            ec2-config-playbook.yml
                    '''
                }
            }
        }

        
        stage('Final Project Verification') {
            steps {
                sshagent(credentials: ['ec2-ansible-ssh']) {
                    sh '''
                        ansible-playbook \
                            -i inventory/production.ini \
                            final-project-check.yml
                    '''
                }
            }
        }
    }
}
