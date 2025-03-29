pipeline {
    agent any
    
    triggers{
        githubPush()
    }
    
    stages {
        stage('cloning repo') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', url: 'https://github.com/Prashanth7993/spring-boot-hello-world.git'
                echo "cloning project done"
            }
        }
        stage('Building Project using dockerfile') {
            steps {
                sh "docker build -t java-app ."
                echo "Building image done."
            }
        }
        stage('Pushing image to hub.docker.com'){
            steps {
                withCredentials([usernamePassword(credentialsId: 'Docker-hub-Credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh "docker login -u $DOCKER_USER -p $DOCKER_PASS"
                        sh "docker tag frontend $DOCKER_USER/java-app:v1"
                        sh "docker push $DOCKER_USER/java-app:v1"
                        echo "Sucefully image pushed to docker hub"
                 }
            }
        }
    }
}
