pipeline {
    agent any

    stages {
        stage('Stage 1') {
            steps {
                echo "Creating file1.txt..."
                sh "echo "File 1 content" >> ./file1.txt"
            }
        }
        stage('Stage 2') {
            steps {
              echo "Creating file1.txt..."
              sh "echo "File 2 conent" >> ./file2.txt"
            }
        }
        stage('Stage 3') {
            steps {
              echo "All done in this Pipeline! exiting..."
            }
        }
    }
}
