pipeline{
    agent any
    environment{
        registry = '076892551558.dkr.ecr.eu-north-1.amazonaws.com/jordan-devops'
        registryCredential = 'jenkins-ecr'
        region = 'eu-north-1'
        dockerimage = ''
    }
    stages{
        stage('checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/jordanehou/argo_logis_project.git'
            }
        }
        
        stage('build image'){
            steps{
                script{
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
            
        }
        stage('docker login'){
            steps{
                script{
                    sh 'aws ecr get-login-password --region "${region}"| docker login --username AWS --password-stdin "${registry}"'
                }
            }
        }
        stage('Deploy image'){
            steps{
                script{
                    dockerImage.push()
                    }
                }
            }
        
    
        /*stage('Deploy image'){
            steps{
                script{
                    docker.withRegistry("https://"+registry,"ecr:eu-north-1:"+registryCredential){
                        dockerImage.push()
                    }
                }
            }
        }
        */
        
    }
}