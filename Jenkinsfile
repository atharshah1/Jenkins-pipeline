    pipeline {
        agent any
        stages {
            stage('Build Application') {
                steps {
                    sh 'yarn'
                    sh 'npm i'
                    sh 'yarn build'
                }
                post {
                    success {
                        echo "Now Archiving the Artifacts...."
                        archiveArtifacts artifacts: '**/build/*'
                    }
                }
            }
            stage('Docker Image of the app'){
                steps{
                    copyArtifacts projectName: '${JOB_NAME}';
                    sh 'ls'
                }
                
            }
        }
    }
