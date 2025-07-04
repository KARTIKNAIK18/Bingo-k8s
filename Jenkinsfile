pipeline{
    agent any


       environment {
        
        SONARQUBE_ENV = 'sonarqube' // Replace with your SonarQube server name from Jenkins settings
    }

    stages{
        stage("git cheackout"){
            steps{
                    git branch: 'main', url: 'https://github.com/KARTIKNAIK18/Bingo-k8s.git'
            }
        }
        // stage("Sonarqube analysis"){
        //     steps{
        //         withSonarQubeEnv("${SONARQUBE_ENV}"){
        //              sh '''
        //                 sonar-scanner \
        //                 -Dsonar.projectKey=Bingo-app \
        //                 -Dsonar.sources=. \
        //                 -Dsonar.host.url=http://localhost:9000 \
        //                 -Dsonar.login=sqp_8cc71bc5604aed6982f02a0c758dbc32e6a0029b 
        //             '''
        //         }
        //     }
        // }
        // stage("Quality Gate"){
        //     steps{
        //         timeout(time: 1, unit: 'HOURS') {
        //         waitForQualityGate abortPipeline: true
        //       }
        //     }
        // }
        stage("docker hub login"){
            steps{
                echo "trying to login docker-hub ........."
                withCredentials([usernamePassword(credentialsId: 'docker-cred',usernameVariable: 'DOCKER_USER',passwordVariable: 'DOCKER_PASS')]){
                sh '''
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    // docker build -t $DOCKER_USER/bingo:latest .
                    // docker push $DOCKER_USER/bingo:latest
                    '''
                }
            }
        }
        stage("push the image to docker-hub"){
            steps{
                echo "uplodaing the image"
                script{
                    sh 'docker docker build -t kartiknaik/bingo:latest .'
                   sh 'docker push $DOCKER_USER/bingo:latest'
                }
                echo "image uploded successfully"
            }
            
        }


    }
}
