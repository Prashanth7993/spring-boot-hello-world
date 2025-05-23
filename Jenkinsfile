pipeline {
    agent any
    
    triggers{
        githubPush()
    }
    
    stages {
        stage('cloning repo') {
            steps {
                // Get some code from a GitHub repository
                deleteDir()
                git branch: 'main', url: 'https://github.com/Prashanth7993/spring-boot-hello-world.git'
                echo "cloning project done"
            }
        }
        stage('Building Project using dockerfile') {
            steps {
                sh 'docker rmi  $(docker images -aq)'
                sh "docker build -t java-app ."
                echo "Building image done."
            }
        }
        stage('Pushing image to hub.docker.com'){
            steps {
                withCredentials([usernamePassword(credentialsId: 'Docker-hub-Credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh "docker login -u $DOCKER_USER -p $DOCKER_PASS"
                        sh "docker tag java-app $DOCKER_USER/java-app:v3"
                        sh "docker push $DOCKER_USER/java-app:v3"
                        echo "Sucefully image pushed to docker hub"
                 }
            }
        }
        stage('Deploying into kubernetes') {
            steps {
                sh "kubectl delete deploy --all"
                sh "kubectl create deploy java-app-kube --image=prashanth7993/java-app:v3 --replicas=3"
            }
        }
    }
}
