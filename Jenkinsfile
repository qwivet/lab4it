pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/qwivet/lab4it.git', 
                     branch: 'main'
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
