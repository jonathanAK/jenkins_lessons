pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo 'build stage started'
                nodejs('Node16') {
                    docker('docker'){
                        sh 'npm install'
                        sh 'docker version'
                    }
                }
            }
        }
        stage('test') {
            steps {
                echo 'test stage started'
            }
        }
    }
}
