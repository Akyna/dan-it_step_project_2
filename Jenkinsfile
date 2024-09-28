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
        DOCKERHUB_CREDENTIALS = credentials('akyna-dockerhub')
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
                // git branch: 'main', url: 'https://github.com/Akyna/dan-it_step_project_2'
                git (
                    url: 'https://github.com/Akyna/dan-it_step_project_2',
                    branch: 'main'
                    )
            }
        }

        stage('Build and run test') {
            steps {
                // or docker run --rm --name app_1_0_1 app:1.0.1 test || echo "Tests failed"; exit 1
                sh '''
                    docker build -t app:1.0.1 .
                    docker run --rm --name app_1_0_1 app:1.0.1 test
                '''
            }
        }
        stage('TEST RESULT') {
            steps {
                sh '''
                    echo "------------------------------"
                    echo $?
                    docker ps -a
                    docker images
                    echo "------------------------------"
                '''
            }
        }
    }
}