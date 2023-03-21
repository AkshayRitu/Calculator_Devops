pipeline {

    environment {
        img=""
    }
    agent any

    stages{

        stage('Github Pull') {
            steps {
                git 'https://github.com/AkshayRitu/Calculator_Devops.git'
            }
        }

      stage('Maven Buid') {
        steps {
            script{
                sh 'mvn clean install'
            }
        }
    }
          stage('Create Docker image') {
        steps {
            script{
                img = docker.build "akshaytakrani11/calculator_devops:latest"
            }
        }
    }

    stage('Push Docker image to DockerHub') {
        steps {
            script{
                docker.withRegistry('',"dockerHub"){
                    img.push()

                }

            }
        }
    }

    stage('Ansible pull docker image from docker hub') {
        steps {
            script{
                sh 'export LC_ALL=en_IN.UTF-8'
            }
            ansiblePlaybook becomeUser: null, colorized: true, disableHostKeyChecking: true, installation: 'Ansible', inventory: 'hosts', playbook: 'playbook.yml', sudoUser: null

        }
    }

    }
}
