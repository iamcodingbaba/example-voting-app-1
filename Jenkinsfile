pipeline{
    agent{
        label "worker"
    }
    stages{
        stage("docker build and push"){
            steps{
                sh '''
                    cd vote
                    aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 271919715952.dkr.ecr.us-east-1.amazonaws.com
                    docker build -t 271919715952.dkr.ecr.us-east-1.amazonaws.com/naam:latest-${BUILD_NUMBER} .
                    docker push 271919715952.dkr.ecr.us-east-1.amazonaws.com/naam:latest-${BUILD_NUMBER}
                    docker stop 271919715952.dkr.ecr.us-east-1.amazonaws.com/naam:latest-${BUILD_NUMBER - 1}
                    docker rm 271919715952.dkr.ecr.us-east-1.amazonaws.com/naam:latest-${BUILD_NUMBER - 1}
                    docker run -itd -p 8080:80 271919715952.dkr.ecr.us-east-1.amazonaws.com/naam:latest-${BUILD_NUMBER}

                    '''
            }
        }
    }
}            
