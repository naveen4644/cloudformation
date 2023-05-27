pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'  // Specify the AWS region
        STACK_NAME = 'DEMO'  // Specify the CloudFormation stack name
        TEMPLATE_FILE = 'devops/demo.yml'  // Specify the CloudFormation template file
      //  PARAMETER_FILE = 'parameters.json'  // Specify the CloudFormation parameter file
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/naveen4644/cloudformation.git'
            }
        }

        stage('Deploy CloudFormation Stack') {
            steps {
                script {
                    // Deploy CloudFormation stack
                    sh 'aws cloudformation deploy --template-file ${TEMPLATE_FILE} --stack-name ${STACK_NAME} --capabilities CAPABILITY_IAM --region ${AWS_REGION}'
                }
            }
        }
    }
}

