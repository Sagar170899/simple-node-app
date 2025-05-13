pipeline {
    agent any
    environment {
        JAVA_HOME = 'C:\\Program Files\\Java\\jdk-<version>'
        PATH = "${env.PATH};${JAVA_HOME}\\bin;C:\\JMeter\\bin"
    }
    stages {
        stage('Install') {
            steps {
                bat 'npm install'
            }
        }
        stage('Start Server') {
            steps {
                bat 'start /B node src/server.js'
                sleep 5
            }
        }
        stage('Performance Test') {
            steps {
                bat 'jmeter -n -t load_test.jmx -l results.jtl'
            }
        }
        stage('Publish Results') {
            steps {
                perfReport sourceDataFiles: 'results.jtl'
            }
        }
    }
}
