pipeline {

  agent any

  options {
    ansiColor('xterm')
  }

  parameters {
    choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Choose Environment')
    choice(name: 'APP_NAME', choices: ['backend', 'frontend'], description: 'Choose AppName')
    string(name: 'VERSION', defaultValue: '', description: 'Version to Deploy')
  }

  stages {

    stage('Deployment') {
      steps {
         dir('APP') {
           git branch: 'main', url: "https://github.com/sampleayeeshagithub/${APP_NAME}"
         }
        dir('HELM') {
          git branch: 'main', url: "https://github.com/sampleayeeshagithub/expense-helm-chart"
          sh 'helm upgrade -i ${APP_NAME} . -f ${WORKSPACE}/APP/helm/${ENV}.yaml --set appVersion=${VERSION}'
        }
      }
    }
  }
  post {
    always {
      cleanWs()
    }
  }

}