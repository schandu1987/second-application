pipeline {
agent any
    stages {
        stage('Code Quality') {
            steps {
                echo 'Sonar Analysis Started'
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://13.127.0.109:9000" -v ".:/usr/src" -e  SONAR_TOKEN="sqa_dbdbafe1b34bf0740ae8bf0e397a00d9b2111d68" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
                echo 'Sonar Analysis Completed'
                }
            }

            stage('Build') {
                steps {
                echo 'Building..'
                sh 'cd webapp && npm install && npm run build'
                echo 'Build is completed'
                }
            }

            stage('Release'){
                steps{
                    echo 'Releaes artifacts'
                    sh 'rm -rf *.zip'
                    sh 'cd webapp && zip dist-${BUILD_NUMBER}.zip -r dist'
                    sh 'cd webapp && curl -v -u admin:admin1234 --upload-file dist-${BUILD_NUMBER}.zip http://13.127.0.109:8081/repository/lms/'
                    echo 'Release completed'
                }
            }

              stage('Deploy') {
                steps {
                    echo 'Deployment'
                    sh 'curl -u admin:admin1234 -X GET http://13.127.0.109:8081/repository/LMS/lms-${BUILD_NUMBER}.zip --output lms-${BUILD_NUMBER}.zip && pwd'
                    
                    
                    echo 'Deployment completed'
                    }

                } 

                

        }
    }
