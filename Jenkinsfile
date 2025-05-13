pipeline {
    agent any
    stages {
        stage('Install') {
            steps {
               // bat 'npm install'
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
