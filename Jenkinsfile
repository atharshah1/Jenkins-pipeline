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
                    copyArtifacts projectName: env.JOB_NAME, filter: "build/*", selector: specific(env.BUILD_NUMBER);
                    sh 'docker build --tag cryptoapp:${BUILD_NUMBER} .'
                }
                
            }
            stage('Deploy to Production'){
                steps{
                    timeout(time:5, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?'
                }
                    sh 'docker container run -d -p 80:80 cryptoapp:${BUILD_NUMBER}'
            }
        }
        }
    }
