pipeline{
    agent {
        label 'worker'
    }
    stages{
        stage("Build and Push"){
            steps{
                sh '''
                    cd vote
                    aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 463470963027.dkr.ecr.ap-south-1.amazonaws.com
                    docker build -t 463470963027.dkr.ecr.ap-south-1.amazonaws.com/demo:vote_v_${BUILD_NUMBER} .
                    docker push 463470963027.dkr.ecr.ap-south-1.amazonaws.com/demo:vote_v_${BUILD_NUMBER}
                    kubectl set image deployment vote vote=463470963027.dkr.ecr.ap-south-1.amazonaws.com/demo:vote_v_${BUILD_NUMBER}
                    kubectl rollout restart deployment vote
                '''
            }
        }
    }
}
