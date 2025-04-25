pipeline {
    agent {
        label 'was' // Harus sesuai dengan label runner Jenkins
    }

    environment {
        WAS_MODE = 'cicd'
        ACCESS_KEY = credentials('$e6e3226d7b38d93f5d80381c8e30e61db91d2d5fd81af425b90af929ebacfdcd') // Ganti dengan ID credential di Jenkins
        SECRET_KEY = credentials('$6dd62277a2aca9c82891b3199bcf10540a0eba15655ff00d1508b5015a17b5e6') // Ganti dengan ID credential di Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Malik-VTI/was-project.git'
            }
        }
    }

    stages {
        stage('Web App Scan') {
            steps {
                script {
                    sh 'docker pull tenable/was-scanner:latest'
                    sh '''
                        docker run \
                            -e WAS_MODE=${WAS_MODE} \
                            -e access_key=${ACCESS_KEY} \
                            -e secret_key=${SECRET_KEY} \
                            -v ${WORKSPACE}/scanner:/scanner \
                            tenable/was-scanner:latest
                    '''
                }
            }
        }
    }
}
