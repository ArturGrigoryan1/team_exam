pipeline {
    agent { label 'jenkins_agent' }
    triggers {
    GenericTrigger(
        genericVariables: [
            [defaultValue: '', key: 'base', regexpFilter: '', value: '$.ref'],
            [defaultValue: '', key: 'action', regexpFilter: '', value: '$.action'],
            [defaultValue: '', key: 'sender', regexpFilter: '', value: '$.pull_request.head.ref'],
            [defaultValue: '', key: 'recipient', regexpFilter: '', value: '$.pull_request.base.ref']
            
            ],
     causeString: 'Triggered on $base',
     token: 'abc123',
     tokenCredentialId: '' )
  }
    stages {
        stage('Check branch name') {
            steps {
                echo 'Hello world'
                echo env.base
                echo env.action
                echo env.sender
                echo env.recipient
                sh 'ls -la'
                
            }
        }
        stage('check merge') {
            when {
                allOf {
                    environment name: 'action', value: 'closed'
                    environment name: 'sender', value: 'staging'
                    environment name: 'recipient', value: 'main'
                }
                
            }
            
            steps {
                echo 'ok'
                sh 'python3 main.py'
            }
        }
        stage('orinak') {
            docker.build("my-image-name")
            
            steps {
                sh 'python --version'
            }
        }
}
}
