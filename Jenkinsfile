pipeline {
    parameters {
        string(name: 'env', defaultValue: 'test', description: '指定要发布的环境，dev/test/master')
        string(name: 'owner', defaultValue: 'jbot', description: '指定用户为:jbot')
        string(name: 'version', defaultValue: 'V1.0.1', description: '指定发布的版本为: V1.0.1')
        string(name: 'apiModule', defaultValue: 'yibot-api', description: '指定要发布的模块名称，yibot-api')
        string(name: 'manageModule', defaultValue: 'yibot-manage', description: '指定要发布的模块名称，yibot-manage')
        string(name: 'apiPortLan', defaultValue: '8101', description: '指定要绑定的内部端口，8101')
        string(name: 'apiPortWan', defaultValue: '10101', description: '指定要绑定的内部端口，10101')
        string(name: 'managePortLan', defaultValue: '8102', description: '指定要绑定的外部端口，8102')
        string(name: 'managePortWan', defaultValue: '10102', description: '指定要绑定的外部端口，10102')
    }
    
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

        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}