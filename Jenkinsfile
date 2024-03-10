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
        
        stage('build Dockerimage') {
            steps{
                script {
                    myimage = docker.build('myimage')
                    myimage.run(-it)
                }
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
                echo 'okay'
                sh 'python3 main.py'
            }
        }
       
        
        
}
}
