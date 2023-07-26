pipeline {
    agent any
    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
    }
    stages {
        stage('Fetch Code from Git') {
            steps {
                // Fetch the code from your Git repository containing Cloud Custodian policies
                git 'https://github.com/your_username/your_repo.git'
            }
        }
        stage('Run Custodian Policy') {
            steps {
              withCredentials([
                    string(credentialsId: 'my-aws-access-key', variable: 'AWS_ACCESS_KEY_ID'),
                    string(credentialsId: 'my-aws-secret-key', variable: 'AWS_SECRET_ACCESS_KEY'),
                    string(credentialsId: 'git_pat', variable: 'GIT_PAT'),
                ]) 
                sh '''
                    # Change directory to the EC2 folder
                    cd EC2

                    # Execute the Cloud Custodian policy
                    custodian run --cache-period 0 --output-dir output0 policy.yml
                '''
            }
        }
    }
}
