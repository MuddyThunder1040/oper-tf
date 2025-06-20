pipeline{
    agent {
        label 'dell'
    }

    /**
     * This Jenkins pipeline builds the Terraform state management project.
     * It checks out the specified branch from the tf_modules repository and performs the build steps.
     * Configure the parameters below to customize the build process.
     */
    parameters {
        string(name: 'Git-Branch', defaultValue: 'main', description: "Branch to checkout from tf_modules repo")
        
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    
                   sh 'Checking out branch: ${params.Git-Branch}'
                }
            }
        }
    }
}