pipeline {
    agent any
    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
    }
    stages {
        stage('Fetch Code from Git') {
            steps {
                // Fetch the code from your Git repository containing Cloud Custodian policies
                git credentialsId: 'GIT_PAT', url: 'https://github.com/Soumya220/custodian_policies.git'
            }
        }
        stage('Run Custodian Policy') {
            steps {
              withCredentials([ 
                    string(credentialsId: 'my-access-key', variable: 'AWS_ACCESS_KEY_ID'),
                    string(credentialsId: 'my-secret-key', variable: 'AWS_SECRET_ACCESS_KEY'),
                    string(credentialsId: 'git_pat', variable: 'GIT_PAT'),
                ]) 
                {
                sh '''
                    # Change directory to the EC2 folder
                    cd EC2

                    # Execute the Cloud Custodian policy
                    /usr/local/bin/custodian run --cache-period 0 --output-dir output0 ec2_running_nonbusiness_hour.yml
                '''
            }
        }
    }
}
}
