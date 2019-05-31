pipeline {
    agent any

    stages {
        stage('Stage 1: check enviroment') {
            steps {
              echo "Check running user"
              sh "whoami"
              sh "who am i"
              echo "Check local directory"
              sh "ls -l"
              echo "Check enviroment variables"
              sh "env"
            }
        }
        stage('Stage 2') {
            steps {
              echo "Check running user"
              sh "whoami"
              echo "Check Ansible version..."
              sh "ansible --version"
            }
        }
        stage('Stage 3') {
            steps {
              echo "All done in this Pipeline! exiting..."
            }
        }
    }
}
