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
                sleep 20
                sh '''
                 CHECK_REZULT=`curl -u admin:admin http://192.168.31.77:9000/api/qualitygates/project_status?projectKey=HelloWoldJavaCheck | jq -r '.projectStatus.status'`
                 if [ $CHECK_REZULT = 'ERROR' ]
                 then
                     echo 'Sonarqube check failed! Fix your code!'
                     exit 1
                 else
                     echo 'Sonarqube check OK! Congratilations!'
                 fi
                '''
            }
        }
        stage('BuildWarFile') {
            steps {
                sh 'jar -cvf helloworld.war *.jsp WEB-INF'
            }
        }
        stage('DeployToDockerImageAndRunIt') {
            steps {
                //sh 'scp helloworld.war tomcat@192.168.31.210:~/webapps/helloworld.war'
                sh '''
                CONTAINER_ID=`docker ps --filter "name=helloworld" -q`
                if [ $CONTAINER_ID ]
                then
                    docker rm -f helloworld
                fi
                IMAGE_ID=`docker images helloworld -q`
                if [ $IMAGE_ID ]
                then
                    docker rmi helloworld
                fi
                docker build -t helloworld .
                docker run --name helloworld -d -p 8000:8080 helloworld
                '''
            }
        } 
    }
}
