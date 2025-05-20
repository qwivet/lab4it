pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/your-username/your-repo.git', 
                     credentialsId: 'github-credentials-id', 
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
            junit 'build/test_report.xml'
        }
    }
}
