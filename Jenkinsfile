pipeline {
    agent { label 'worker' }
    
    environment {
        DOCKERHUB_CREDENTIALS = credentials('akyna-dockerhub')
        APP_NAME = "akyna/step_project_2"
    }

    stages {
        stage('SCM Checkout') {
            steps {
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
                    docker build -t $APP_NAME:$BUILD_NUMBER .
                    docker run --rm --name step_project_2 $APP_NAME:$BUILD_NUMBER test
                '''
            }
        }
        stage('Login to Dockerhub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push image') {
            steps {
                sh 'docker push $APP_NAME:$BUILD_NUMBER'
            }
        }
        stage('Cleaning up') { 
            steps { 
                sh 'docker rmi $APP_NAME:$BUILD_NUMBER'
            }
        } 
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}