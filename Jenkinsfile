pipeline {
    agent any

    environment {
                APP_NAME = "326927831581.dkr.ecr.us-east-1.amazonaws.com/argocicd"
            }

    stages {
        stage ('Update Kubernetes deployment file') {
            steps {  
                echo 'updating app-deploy.yaml file' 
                script {
                        dir ('k8s') {
                        sh """
                        cat app-deploy.yml
                        sed -i 's/argocicd.*/argocicd:${BUILD_NUMBER}/g' app-deploy.yml
                        cat app-deploy.yml
                        """
                    }
                }
            } 
        }
        
        
        stage ('Push the changed deployment yaml file to Git') {
            steps {  
                echo 'Pushing changed files to Git' 
                script {
                        dir ('k8s') {
                        sh """
                        touch samplefile.txt
                        git config --global user.name "Danny"
                        git config --global user.email "dangeo36@gmail.com"
                        git add .
                        git commit -m "update app-deploy"
                        """
                        withCredentials([string(credentialsId: 'git-creds', variable: 'GIT_TOKEN')]) {
                             sh "git push origin HEAD:main"
                        }
                    }
                }
            } 
        }
    }
}
