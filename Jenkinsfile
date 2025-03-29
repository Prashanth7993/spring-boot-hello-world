pipeline {
    agent any
    
    triggers{
        githubPush()
    }
    
    stages {
        stage('cloning repo') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/Prashanth7993/spring-boot-hello-world.git'
                echo "cloning project done"
            }
        }
        stage('Building Project using dockerfile') {
            steps {
                sh "docker build -t java-app ."
                echo "Building image done."
            }
        }
    }
}
