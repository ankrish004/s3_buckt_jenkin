pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        CLUSTER_NAME = 'heartfelt-bee-7l0iha'
        REACT_APP_VERSION = "1.0.$BUILD_ID"
        APP_NAME = 'newjenkinapp'
    }

    stages {

        stage('BUILD') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                node --version
                npm --version
                npm ci
                npm run build
                '''
            }
        }
        
        stage('docker image build') {
            steps {
                sh 'docker build -t $APP_NAME:$REACT_APP_VERSION .'
            }
        }
        
        /* 
        stage('AWS-cli') {
            agent {
                docker {
                    image 'amazon/aws-cli:2.34.26'
                    args "-u root --entrypoint=''"
                }
            }

            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'aws-id',
                        usernameVariable: 'AWS_ACCESS_KEY_ID',
                        passwordVariable: 'AWS_SECRET_ACCESS_KEY'
                    )
                ]) {
                    sh '''
                    yum install jq -y  

                    TD_REVISION=$(aws ecs register-task-definition \
                        --cli-input-json file://aws/task-define.json \
                        | jq -r '.taskDefinition.revision')

                    echo "Revision: $TD_REVISION"

                    aws ecs update-service \
                        --cluster $CLUSTER_NAME \
                        --service learnapp-TaskDefinition-prod-service-hsylsait \
                        --task-definition learnapp-TaskDefinition-prod:$TD_REVISION \
                        --force-new-deployment
                    '''
                }
            }
        }*/
    }
}