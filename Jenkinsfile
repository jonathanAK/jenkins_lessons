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
                    BRANCH_NAME == 'feature_color'
                }
            }
            steps {
                echo 'deploy stage started'
                withAWS(region:'<AWS Region: like us-west-2>', credentials:'RDG AWS') {
                    s3Upload(bucket:"my-bucket", path:'demo/', includePathPattern:'**/*', workingDir:'demo')
                }
            }
        }
    }
}
