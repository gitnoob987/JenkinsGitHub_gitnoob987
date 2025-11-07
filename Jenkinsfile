pipeline {
    agent any
    environment {
        TF_VAR_gcp_project = "qwiklabs-gcp-00-6dfa7a7fad3e" // replace with your project ID ...
        TF_VAR_bucket = "tf-remote-state-student_01_d37aed5acaf8-1081-26869"
    }
    stages {
        stage('Terraform Init') {
            steps {
                withCredentials([file(credentialsId: 'gcp-svc-acct', variable: 'GOOGLE_CLOUD_KEYFILE_JSON')]) {
                    sh '''
                    export GOOGLE_APPLICATION_CREDENTIALS=$GOOGLE_CLOUD_KEYFILE_JSON
                    terraform init
                    '''
                }
            }
        }
        stage('Terraform Plan') {
            steps {
                withCredentials([file(credentialsId: 'gcp-svc-acct', variable: 'GOOGLE_CLOUD_KEYFILE_JSON')]) {
                    sh '''
                    export GOOGLE_APPLICATION_CREDENTIALS=$GOOGLE_CLOUD_KEYFILE_JSON
                    terraform plan
                    '''
                }
            }
        }
        stage('Terraform Apply') {
            steps {
                withCredentials([file(credentialsId: 'gcp-svc-acct', variable: 'GOOGLE_CLOUD_KEYFILE_JSON')]) {
                    sh '''
                    export GOOGLE_APPLICATION_CREDENTIALS=$GOOGLE_CLOUD_KEYFILE_JSON
                    terraform apply -auto-approve
                    '''
                }
            }
        }
    }
}
