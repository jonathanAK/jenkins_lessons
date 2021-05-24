pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo 'build stage started'
                nodejs('Node16') {
                    sh 'npm install'
                }
            }
        }
        stage('test') {
            steps {
                echo 'test stage started'
            }
        }
        stage('deploy to s3') {
            when{
                expression {
                    BRANCH_NAME == 'master'
                }
            }
            steps {
                echo 'deploy stage started'
                withAWS(region:'<AWS Region: like us-west-2>', credentials:'RDG AWS') {
                  s3Delete(bucket: 'psi2021-demo-public', path:'**/*')
                  s3Upload(file:'./demo', bucket:'psi2021-demo-public', path:'/')
                }
            }
        }
    }
}
