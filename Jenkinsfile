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
            environment{
                AWS_TOKEN = credentials('AWS')
            }
            when{
                expression {
                    BRANCH_NAME == 'feature_color'
                }
            }
            steps {
                echo 'deploy stage started'
                withAWS(region:'us-east-1', credentials:'AWS') {
                    s3Upload(bucket:"my-bucket", path:'demo/', includePathPattern:'**/*', workingDir:'demo')
                }
            }
        }
    }
}
