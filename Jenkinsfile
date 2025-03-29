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
                sh "docker tag java-app prashanth7993/java-app:v1'
                sh "docker push prashanth7993/java-app:v1"
                echo "Sucessfully image pushed to docker hub"
            }
        }
    }
}
