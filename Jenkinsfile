pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    }
    options {
        timeout(time: 1, unit: 'HOURS')
        disableConcurrentBuilds()
    }
    
    // build
    stages {
        stage('Init') {
            steps {
                sh """
                    cd 01-vpc
                    terraform init -reconfigure
                """
            }
        }
        stage('plan') {
            steps {
                sh """
                    cd 01-vpc
                    terraform plan
                """
            }
        }
        stage('Deploy') {
            input {
                message "Should we continue?"
                ok "Yes, we should."
                // submitter "alice,bob"
                // parameters {
                //     string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                // }
            }
            steps {
                sh """
                    cd 01-vpc
                    terraform apply -auto-approve
                """
            }
        }
        
    }
    // Post build means build ipoena tharuwatha em cheyali 
    post { 
        always { 
            echo 'I will always say Hello again!'
        }
        failure { 
            echo 'This runs when pipeline is failed , used generally to send some alerts !'
        }
        success { 
            echo 'I will say Hello when pipeline is success !'
        }
    }
}