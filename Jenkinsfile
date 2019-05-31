pipeline {
    agent any

    stages {
        stage('Deploy code to PE') {
            steps {
                sh '/opt/puppetlabs/bin/puppet-code deploy production --wait'
            }
        }
        stage('Checkpoint configuration') {
            steps {
                sh "/opt/puppetlabs/bin/puppet-task run yang_ietf::checkpoint target='cat9k-puppet' --nodes 'cisco-pe-demo.localhost'"
            }
        }
        stage('Execute Puppet Device') {
            steps {
                sh "/opt/puppetlabs/bin/puppet-task run puppet_device target='cat9k-puppet' --nodes 'cisco-pe-demo.localhost'"
            }
        }
        stage('Validate Changes') {
            steps {
                echo 'Testing....'
                script {
                    try {
                        sh "/opt/puppetlabs/bin/puppet-task run yang_ietf::forbidden target='cat9k-puppet' forbidden='apic' --nodes 'cisco-pe-demo.localhost'"
                    } catch (error) {
                        sh "/opt/puppetlabs/bin/puppet-task run yang_ietf::rollback target='cat9k-puppet' --nodes 'cisco-pe-demo.localhost'"
                        error("Changes failed testing.  Rolled back.")
                    }
                }
            }
        }
        stage('Copy run-start') {
            steps {
                sh "/opt/puppetlabs/bin/puppet-task run yang_ietf::saveconfig target='cat9k-puppet' --nodes 'cisco-pe-demo.localhost'"
            }
        }
    }
}
