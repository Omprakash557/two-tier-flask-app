pipeline {
    agent any
    stages{
        stage("clone code"){
            steps{
                git branch:"master",url:"https://github.com/Omprakash557/two-tier-flask-app.git"
            }
        }
        stage("build"){
            steps{
                sh "docker build -t my-app-flask ."
            }
        }
        stage("test"){
            steps{
                echo "dev ho gya"
            }
        }
        stage("Push Code To Docker"){
            steps {withCredentials([usernamePassword(
                credentialsId:"extraone5464",
                passwordVariable:"PASS",
                usernameVariable:"USER")]){
                    sh '''
                    echo "$PASS" | docker login -u "$USER" --password-stdin
                    docker image tag my-app-flask "$USER"/my-app-flask:latest
                    docker push "$USER"/my-app-flask:latest
                    '''
                }
            }
        }
        stage("deploy"){
            steps {
                sh "docker-compose down"
                sh "docker-compose up -d"
            }
        }
    }
}
