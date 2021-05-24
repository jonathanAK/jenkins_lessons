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
                s3Upload consoleLogLevel: 'INFO', dontSetBuildResultOnFailure: false, dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'psi2021-demo-public', excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: false, selectedRegion: 'us-iso-east-1', showDirectlyInBrowser: false, sourceFile: './demo', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'FAILURE', profileName: 'S3_jenkins_profile', userMetadata: []
            }
        }
    }
}
