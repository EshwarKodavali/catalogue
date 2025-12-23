pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    }
    environment {
        COURSE = "Jenkins"
        appVersion = ""
    }
    options {
        timeout(time: 10, unit: 'MINUTES') 
        disableConcurrentBuilds()
    }
    // This is build section
    stages {
        stage('Read Version') {
            steps {
                script{
                    def packageJSON = readJSON file: 'package.json'
                    appVersion = packageJSON.version
                    echo "app version: ${appVersion}"
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                script{
                    sh """
                        npm install
                    """
                }
            }
        }
        stage('Build Image') {
            steps {
                script{
                    sh """
                        docker build -t catalogue:${appVersion} .
                        docker images
                    """
                }
            }
        
        stage('Test') {
            steps {
                script{
                    sh """
                    echo "Testing"
                    """
                }
            }
        }
        stage('Deploy') {
                        input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
                        }
            steps {
                script{
                   sh """
                    echo "Deploying"
                    """
                }
            }
        }
    }
    post{
        always{
            echo 'I will always say Hello again!'
            cleanWs()
            }
        success{
            echo 'i will run when i am success'
        }
        failure{
            echo 'i will run when i am failure'
        }
        aborted {
            echo 'pipeline is aborted'
        }        
    }
}