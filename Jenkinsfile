//properties([
//        pipelineTriggers([
//                githubPush()
//        ])
//])
//properties {
//    pipelineTriggers {
//        triggers {
//            cron {
//                spec('@midnight')
//            }
//            upstream{
//                upstreamProjects('someJob')
//                threshold('SUCCESS')
//            }
//        }
//    }
//}

pipeline {
    agent { label 'worker' }
//    triggers {
//        githubPush()
//    }


    environment {
        AWS_REGION = 'eu-west-1'
        ECR_REPO = 'flask-api'
        AWS_ACCOUNT_ID = '381492243289'
        URL_REGISTRY = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com"
        IMAGE_TAG = "${URL_REGISTRY}/${ECR_REPO}"
    }

    stages {
        // 1. Checkout from SCM (Git)
        stage('SCM Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Akyna/dan-it_step_project_2'
            }
        }

        stage('Echo') {
            steps {
                sh '''
                    docker --version
                    exit 123
                    echo "EXIT_CODE=$?"
                '''
            }
        }
        stage('TEST RESULT') {
            steps {
                sh '''
                    echo "DONE 2"
                '''
            }
        }
    }
}