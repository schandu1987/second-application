pipeline {
agent any
    stages {
        stage('Code Quality') {
            steps {
                echo 'Sonar Analysis Started'
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://13.234.78.44:9000" -v ".:/usr/src" -e  SONAR_TOKEN="sqa_dbdbafe1b34bf0740ae8bf0e397a00d9b2111d68" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
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
                    sh 'zip lms.zip -r dist/*'
                    sh 'curl -v -u admin:admin1234 --upload-file  lms.zip http://13.234.78.44:8081/repository/LMS/'
                    echo 'Artifacts successfull'
                }
            }

        }
    }
