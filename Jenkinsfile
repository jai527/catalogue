pipeline{
    agent any
    }
    /* environment{
        COURSE = "jenkins"
    } */
    options {
    //disableConcurrentBuilds()
    timeout(time: 5, unit: 'MINUTES')
    }
    /* parameters {
        string(name: 'USERNAME', defaultValue: 'admin', description: 'Enter your username')
        booleanParam(name: 'DEBUG_MODE', defaultValue: false, description: 'Enable debug mode?')
        choice(name: 'ENVIRONMENT', choices: ['dev', 'qa', 'prod'], description: 'Select environment')
        text(name: 'NOTES', defaultValue: '', description: 'Additional notes')
        password(name: 'SECRET_KEY', defaultValue: '', description: 'Enter secret key')
    } */
    stages{
        stage('Read version'){
            steps{
                script{
                    def packageJSON = readJSON file: 'package.json'
                    def packageJSONVersion = packageJSON.version
                    echo packageJSONVersion
                }

            }

        }
        stage('install dependance'){
            steps{
                script{
                    sh """
                    npm install
                    """
                }
            }
        }
        stage('Build Docker Image'){
            steps{
                script{
                    sh """
                    docker build -t catalogue:1.0.0 
                    """
                }
            }
        }
    }
    // post biuld 
    post{
        always{
            echo 'I will always say hell again'
        }
        success{
            echo 'pipeline is success'
        }
        failure{
            echo 'pipeline is failure'
        }
    }
}