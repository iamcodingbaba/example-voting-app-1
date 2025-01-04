pipeline{
    agent{
        label "slave"
    }
    stages{
        stage("docker build and push"){
            steps{
                sh '''
                    cd vote
                    aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 271919715952.dkr.ecr.us-east-1.amazonaws.com
                    docker build -t 271919715952.dkr.ecr.us-east-1.amazonaws.com/coding_baba:latest-${BUILD_NUMBER} .
                    docker push 271919715952.dkr.ecr.us-east-1.amazonaws.com/coding_baba:latest-${BUILD_NUMBER}
                    docker stop $(docker ps -a -q)
                    docker run -itd -p 627:80 271919715952.dkr.ecr.us-east-1.amazonaws.com/coding_baba:latest-${BUILD_NUMBER}

                    '''
            }
        }
    }
}            
