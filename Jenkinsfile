
pipeline {
    agent { label 'worker' }
//    triggers {
//        githubPush()
//    }
    options {
        pipelineTriggers {
            triggers {
                githubPush()
            }
        }
    }

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
    }
}