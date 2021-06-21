pipeline {
  agent any
  tools {
      // Install the Maven version configured as "maven_home" and add it to the path.
      maven "maven_home"
  }
  stages {
    stage('Build and Test') {
      parallel {

        stage('Checkout On Slave 1') {
          agent {
            node {
              label 'Slave-1'
            }
          }
          steps {
            git(url: 'https://github.com/ishani-jaswal/softmax-filters.git', branch: 'master')
          }
        }
        
        stage('Compile and Package On Slave 1') {
          agent {
            node {
              label 'Slave-1'
            }
          }
          steps {
            sh "mvn clean package"
          }
        }

        stage('Checkout On Slave 2') {
          agent {
            node {
              label 'Slave-2'
            }
          }
          steps {
            git(url: 'https://github.com/ishani-jaswal/softmax-filters.git', branch: 'master')
          }
        }
        
        stage('Unit Test On Slave 2') {
          agent {
            node {
              label 'Slave-2'
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
