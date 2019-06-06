pipeline {
    agent any

    stages {
        stage('1: Update code from GitHub') {
            steps {
              echo "Check enviroment "
              sh "whoami"
              sh "who am i"
              sh "ls -l"
              sh "env"
              echo "Pull code from GitHub"
              sh 'git pull origin master'
            }
        }
        stage('2: Verify before pushing changes to Production') {
            steps {
              echo "Running Ansible playbook with Before snapshot"
              script {
                    try {
                      sh "ansible-playbook fwd-ansible/test_esx_traffic.yml --extra-vars=@fwd-ansible/deployments/test-snapshots-before.yml --extra-vars=expected_check_status=FAIL"
                    } catch (error) {
                    error("Ansible Playbook failed!!!")
                    }
                }
            }
        }
        stage('3: Pushing changes to production' ) {
            steps {
              echo "Sleeping for a while..."
              sh "sleep 10"
            }
        }
        stage('4: Verify after the changes have been pushed to Production') {
            steps {
              echo "Running Ansible playbook with After snapshot"
              script {
                    try {
                      sh "ansible-playbook fwd-ansible/test_esx_traffic.yml --extra-vars=@fwd-ansible/deployments/test-snapshots-after.yml --extra-vars=expected_check_status=PASS"
                    } catch (error) {
                    error("Ansible Playbook failed!!!")
                    }
                }
            }
        }
    }
}
