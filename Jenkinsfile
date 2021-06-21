pipeline {
  agent any
  tools {
      // Install the Maven version configured as "M3" and add it to the path.
      maven "M3"
  }
  stages {
    stage('Build and Test') {
      parallel {

        stage('Checkout On Slave 1') {
          agent {
            node {
              label 'slave-1'
            }
          }
          steps {
            git(url: 'https://github.com/ishani-jaswal/softmax-filters.git', branch: 'master')
          }
        }
        
        stage('Compile and Package On Slave 1') {
          agent {
            node {
              label 'slave-1'
            }
          }
          steps {
            sh "mvn clean package"
          }
        }

        stage('Checkout On Slave 2') {
          agent {
            node {
              label 'slave-2'
            }
          }
          steps {
            git(url: 'https://github.com/ishani-jaswal/softmax-filters.git', branch: 'master')
          }
        }
        
        stage('Unit Test On Slave 2') {
          agent {
            node {
              label 'slave-2'
            }
          }
          steps {
            sh "mvn test"
          }
        }

      }
    }

  }
}
