pipeline {
    agent {
        label 'dell-worker'
    }
    parameters {
        string(name: 'Git-Branch', defaultValue: 'main', description: "Git branch to build")
        choice(name: 'Terraform-Operation', choices: ['plan', 'apply','destroy','show'], description: "Terraform operation to perform")
    }

    stages {
        stage ('Git Checkout') {
            steps {
                git branch: "${params.Git-Branch}", url: 'https://github.com/MuddyThunder1040/tf_modules.git'
            }
        }
        stage ('Terraform operation') {
            steps {
                script {
                    def operation = params.Terraform-Operation
                    if (operation == 'plan') {
                        sh 'terraform init'
                        sh 'terraform plan'
                    } else if (operation == 'apply') {
                        sh 'terraform init'
                        sh 'terraform apply -auto-approve'
                    } else if (operation == 'destroy') {
                        sh 'terraform init'
                        sh 'terraform destroy -auto-approve'
                    } else if (operation == 'show') {
                        sh 'terraform init'
                        sh 'terraform show'
                    } else {
                        error "Invalid Terraform operation: ${operation}"
                    }
                }
            }
        }
    }

}
