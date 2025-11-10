pipeline{
    agent any // decided which node to run

    tools {
        jdk 'java-17'
        maven 'maven'
    }

    environment {
        IMAGE_NAME = manojkrishnappa/itkannaDigaru-blogpost:${GIT_COMMIT}
    }

    stages{
        stage('git-checkout'){
            steps{
                git url: 'https://github.com/ManojKRISHNAPPA/ITKannadigaru-Java-based-app.git', branch: 'prod'
            }
            
        }

        stage('Compile'){
            steps{
                sh '''
                    mvn compile
                '''
            }
        }
        stage('packaging'){
            steps{
                sh '''
                    mvn clean package
                '''
            }
        }
        stage('docker-build'){
            steps{
                sh '''
                    docker build -t ${IMAGE_NAME} .
                '''
            }
        }
        stage('Docker-testing'){
            steps{
                sh '''
                    docker run -it -d --name itkannaDigaru-blogpost-test -p 9000:8080 ${IMAGE_NAME}
                '''
            }
        }        

    }
}