pipeline {
    agent {
        docker {
            image 'maven:3.5.3-jdk-8'
            args '-v /var/jenkins_home/docker/data/maven/root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
    }
}