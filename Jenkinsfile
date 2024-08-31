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