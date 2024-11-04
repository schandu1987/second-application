   pipeline {
        agent any
        stages {
          stage("Code anylsis using SonarQube analysis") {
               steps {
               {
                sh 'sudo docker run --rm -e SONAR_HOST_URL="http://65.2.30.142:9000/" -e SONAR_LOGIN="sqa_83f8b65a59e5b5c047f5245f10b11017bd8d528c" -v ".:/usr/src" sonarsource/sonar-scanner-cli:5.0 -Dsonar.projectKey=lms'
              }
            }
          }
          
        }
      }