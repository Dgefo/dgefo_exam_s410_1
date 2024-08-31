pipeline {
    agent any 
    stages {
        stage('ThisIsExam') {
            steps {
                echo 'Это экзамен. Просто работа с гитхаб!' 
            }
        }
        stage('semgrep-scan') {
          steps {
            script {
              sh '''
               # Ставим питон и пакетиеи
               apk add --no-cache python3 py3-pip py3-virtualenv
               python3 -m venv venv
               source venv/bin/activate
               pip install semgrep
               semgrep --config auto . --json > output-semgrep.json
             '''
            }
          archiveArtifacts artifacts: 'output-semgrep.json', allowEmptyArchive: true
          }
        }
        stage('trivy'){
          agent {
                label 'dind'
          }
          steps {
            script {
              sh '''
              docker run aquasec/trivy repo https://github.com//Dgefo/dgefo_exam_s410_1 -f json -o json > trivy.json
              echo 'Здесь trivy!' 
              '''
              archiveArtifacts artifacts: 'trivy.json', allowEmptyArchive: true
            }
          }
        }
    }
}