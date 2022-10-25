pipeline {
    agent any
    stages {
        stage('TestWithSonarQube') {
            steps {
                sh '''
                ~/sonar-scanner-4.7.0.2747-linux/bin/sonar-scanner \
                -Dsonar.projectKey=HelloWoldJavaCheck \
                -Dsonar.sources=. \
                -Dsonar.host.url=http://192.168.31.77:9000 \
                -Dsonar.login=sqp_da879a3eb176f14d19821a8f5508c6a233e73162
                '''
            }
        }
        stage('BuildWarFile') {
            steps {
                sh 'jar -cvf helloworld.war *.jsp WEB-INF'
            }
        }
        stage('DeployToTomcatServer') {
            steps {
                sh 'docker cp helloworld.war tomcat:/usr/local/tomcat/webapps'
            }
        } 
    }
}
