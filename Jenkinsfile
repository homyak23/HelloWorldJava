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
                //sh 'scp helloworld.war tomcat@192.168.31.210:~/webapps/helloworld.war'
                sh '''
                docker stop helloworld
                docker rm helloworld
                docker rmi helloworld
                docker build -t helloworld .
                docker run --name helloworld -d -p 8000:8080 helloworld
                '''
            }
        } 
    }
}
