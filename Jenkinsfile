pipeline {
    agent any

    /* environment {
        COURSE = "jenkins"
    } */

    options {
        timeout(time: 5, unit: 'MINUTES')
    }

    /* parameters {
        string(name: 'USERNAME', defaultValue: 'admin', description: 'Enter your username')
        booleanParam(name: 'DEBUG_MODE', defaultValue: false, description: 'Enable debug mode?')
        choice(name: 'ENVIRONMENT', choices: ['dev', 'qa', 'prod'], description: 'Select environment')
        text(name: 'NOTES', defaultValue: '', description: 'Additional notes')
        password(name: 'SECRET_KEY', defaultValue: '', description: 'Enter secret key')
    } */

    stages {

        stage('Read version') {
            steps {
                script {
                    def packageJSON = readJSON file: 'package.json'
                    def packageJSONVersion = packageJSON.version
                    echo "${packageJSONVersion}"
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh '''
                        npm install
                    '''
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh '''
                        sh '''
                            docker build -t catalogue:1.0.0 -f docker/Dockerfile .
                    '''
                }
            }
        }
    }

    post {
        always {
            echo 'I will always say hello again'
        }

        success {
            echo 'Pipeline is successful'
        }

        failure {
            echo 'Pipeline failed'
        }
    }
}