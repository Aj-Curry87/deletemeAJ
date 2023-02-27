pipeline {
    agent any

    
    stages {
        stage('Login, Build and Push'){
            steps {
                script{
                    //sign into docker, build image, and push image to dockerhub
                    withDockerRegistry(credentialsId: 'Docker') {
                        docker.build('bjgomes/flaskapp').push('latest')
                    }
                }
            }
        }
        stage('AWS Commands'){
            steps {
                script {
                    // sign into AWS
                    withAWS(credentials: 'AWS_Credentials', region: 'us-east-1'){ 
                        sh 'aws sts get-caller-identity'
                    }
                }
            }
        }
        stage('Kubernetes login'){
            steps{
                script{
                    //Exact same for everyone in the class except the credential variable, use your own credential variable id.  Update kubeconfig in container
                    withAWS(credentials: 'AWS_Credentials', region: 'us-east-1') {
                        sh 'aws eks update-kubeconfig --region us-east-1 --name VETTEC'
                    }
                }
            }
        }
    }
}


