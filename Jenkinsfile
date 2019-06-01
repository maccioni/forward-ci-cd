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
        stage('Stage 2: Verify before pushing changes to Production') {
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
        stage('Stage 3: Pushing changes to production' ) {
            steps {
              echo "Sleeping for a while..."
              sh "sleep 120"
            }
        }
        stage('Stage 4: Verify after the changes have been pushed to Production') {
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
