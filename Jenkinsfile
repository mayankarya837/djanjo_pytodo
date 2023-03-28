pipeline{
    agent any

    stages{
        stage("code"){
            echo "copying url"
            git url:"https://github.com/mayankarya837/djanjo_pytodo.git", branch:"develop"
        }
        stage("Build"){
            sh "docker build . -t mayankaryta837/todo:latest"
        }
        stage("Push"){
            withCredentials([usernamePassword(credentialsId:'deockerHub',passwordvariable:'dockerpass',usernamevariable:'dockeruser')]){
                sh 'docker login -u ${env.dockeruser} -p ${env.dockerpass}'
                sh 'docker push mayankaryta837/todo:latest'
            }
        }
        stage("Deploy"){
            sh 'docker-compose up --force-recreate --no-deps --build web'
        }                        
    }

}