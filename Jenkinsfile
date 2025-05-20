pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'a7009af2-a730-4e5e-92df-6dc52c2e3977', url: 'https://github.com/qwivet/lab4it.git'
            }
        }

        stage('Build') {
            steps {
                sh '''
                    mkdir -p build
                    cd build
                    cmake .. -DCMAKE_BUILD_TYPE=Release
                    make
                '''
            }
        }

        stage('Test') {
            steps {
                sh 'cd build && ./test_repos --gtest_output="xml:test_report.xml"'
            }
        }
    }

    post {
        always {
            junit 'test_report.xml'
        }
    }
}
