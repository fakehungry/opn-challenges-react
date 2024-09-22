pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
              docker {
                image 'node:18-alpine'
                reuseNode true
              }
            }
            steps {
                sh '''
                    yarn install --frozen-lockfile
                '''
            }
        }

        stage('Test') {
            agent {
              docker {
                image 'node:18-alpine'
                reuseNode true
              }
            }
            steps {
                sh '''
                    yarn test --coverage
                '''
            }
        }
    }

    post {
      always {
        junit 'junit.xml'
        publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'coverage/lcov-report', reportFiles: 'index.html', reportName: 'Coverage Report', reportTitles: '', useWrapperFileDirectly: true])
      }
    }
}
