pipeline {
    agent any
    stages {
        stage('TestWithSonarQube') {
            steps {
                sh '''
                /var/lib/jenkins/sonar-scanner-4.7.0.2747-linux/bin/sonar-scanner \
                -Dsonar.projectKey=HelloWoldJavaCheck \
                -Dsonar.sources=/var/lib/jenkins/workspace/JobForTest1 \
                -Dsonar.host.url=http://192.168.31.77:9000 \
                -Dsonar.login=sqp_da879a3eb176f14d19821a8f5508c6a233e73162
                '''
            }
        }
        stage('BuildJavaFile') {
            steps {
                sh 'javac HelloWorld.java'
            }
        } 
    }
}
