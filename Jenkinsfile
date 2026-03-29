pipeline {
    agent any  // Runs on any available Jenkins agent
    environment {
        // Jenkins credentials IDs for AWS
        AWS_ACCESS_KEY_ID = credentials('Access key 1')
        AWS_SECRET_ACCESS_KEY = credentials('AKIA6ARVRU5V74CEIDIW')
        AWS_DEFAULT_REGION = 'ap-south-1'
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out code..."
                git 'https://github.com/RahulSolanki007/cloudformation.git'
            }
        }

        stage('Validate Template') {
            steps {
                echo "Validating CloudFormation template..."
                sh '''
                aws cloudformation validate-template \
                    --template-body file://template.yaml
                '''
            }
        }


        stage('Deploy CloudFormation') {
            steps {
                echo "Deploying CloudFormation stack..."
                sh '''
                aws cloudformation deploy \
                    --template-file template.yaml \
                    --stack-name my-stack \
                    --capabilities CAPABILITY_NAMED_IAM
                '''
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully ✅"
        }
        failure {
            echo "Pipeline failed ❌"
        }
    }
}