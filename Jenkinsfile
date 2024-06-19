pipeline {
    agent any

    environment {
        CONTAINER_NAME = "my-app"
        DATABASE_NAME = "MyDatabase"
        DATABASE_PASSWORD = "Bao@123"
        DATABASE_ROOT_PASSWORD = "root_password"
        DATABASE_USER = "admin"
    }

    stages {
        stage('Checkout') {
            steps {
                // Lấy mã nguồn từ repository
                git credentialsId: 'bao126nvc', url: 'https://github.com/iamBao00/cdcnpm.git', branch: 'main'
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    // Xây dựng và triển khai bằng Docker Compose
                    bat 'docker-compose down'



                    // Chỉ khởi động lại dịch vụ WordPress
                    bat 'docker-compose up --build'
                }
            }
        }

        stage('Post-deploy Cleanup') {
            steps {
                // Bất kỳ bước dọn dẹp nào sau triển khai, nếu cần
                bat 'docker system prune -f'
            }
        }
    }

    post {
        always {
            // Luôn luôn lưu trữ log
            archiveArtifacts artifacts: '**/logs/**', allowEmptyArchive: true
        }
    }
}