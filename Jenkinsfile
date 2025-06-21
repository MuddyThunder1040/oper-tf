pipeline {
    agent { label 'dell' }

    parameters {
        choice(name: 'TF_ENV', choices: ['Local', 'dev', 'prod'], description: 'Terraform Environment Folder')
        string(name: 'TF_VARS_FILE', defaultValue: 'local.tfvars', description: 'TF Vars filename inside environment folder')
    }

    environment {
        MODULE_REPO = 'https://github.com/MuddyThunder1040/tf-topology-modules.git'
        TFVARS_REPO = 'https://github.com/MuddyThunder1040/tf-topology.git'
    }

    stages {
        stage('Checkout Repos') {
            steps {
                deleteDir()
                dir('modules') {
                    git url: "${env.MODULE_REPO}", branch: 'main'
                }
                dir('tfvars') {
                    git url: "${env.TFVARS_REPO}", branch: 'main'
                }
            }
        }

        stage('Terraform Init & Plan') {
            steps {
                dir('modules') {
                    sh 'terraform init'
                    sh "terraform plan -var-file=\"../tfvars/${params.TF_ENV}/${params.TF_VARS_FILE}\""
                }
            }
        }

        stage('Terraform Apply') {
            when { branch 'main' }
            steps {
                dir('modules') {
                    sh "terraform apply -auto-approve -var-file=\"../tfvars/${params.TF_ENV}/${params.TF_VARS_FILE}\""
                }
            }
        }
    }
}
