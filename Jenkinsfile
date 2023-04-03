pipeline{
    agent any

    stages{
        stage("code"){
            steps{
                echo "copying url"
                git url:"https://github.com/mayankarya837/djanjo_pytodo.git", branch:"develop"
            }
        }
        stage("Build"){
            steps{
                sh "docker build . -t mayankaryta837/todo:latest"
            }
        }
        stage("Push"){
            steps{
                withCredentials([usernamePassword(credentialsId:'dockerHub',passwordVariable:'dockerpass',usernameVariable:'dockeruser')]){
                    sh 'docker login -u ${env.dockeruser} -p ${env.dockerpass}'
                    sh 'docker push mayankaryta837/todo:latest'
                }
            }
        }
        stage("Deploy"){
            steps{
                sh 'docker-compose up --force-recreate --no-deps --build web'
            } 
        }                       
    }

}