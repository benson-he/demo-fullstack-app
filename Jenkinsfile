pipeline {
    agent {
        label 'tyy-221' // 指定在远程节点 tyy-221 上运行
    }
    tools {
        maven ''apache-maven-3.9.1 // 使用在 Global Tool Configuration 中配置的 Maven
        nodejs ''node-23-10 // 使用在 Global Tool Configuration 中配置的 NodeJS
    }
    stages {
        stage('Checkout') {
            steps {
                // 检出代码（假设代码在 Git 仓库中）
                checkout scm
            }
        }
        stage('Build Backend') {
            steps {
                dir('backend') {
                    // 使用 Maven 构建后端项目
                    sh 'mvn clean install'
                }
            }
        }
        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    // 使用 npm 构建前端项目
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }
        stage('Test Backend') {
            steps {
                dir('backend') {
                    // 运行后端测试（如果有）
                    sh 'mvn test'
                }
            }
        }
        stage('Test Frontend') {
            steps {
                dir('frontend') {
                    // 运行前端测试（如果有）
                    sh 'npm test'
                }
            }
        }
        stage('Deploy') {
            steps {
                // 简单的部署步骤（可以根据需求扩展）
                echo 'Deploying application...'
                // 示例：将构建产物复制到某个目录
                sh 'mkdir -p /tmp/demo-app'
                sh 'cp backend/target/*.jar /tmp/demo-app/backend.jar'
                sh 'cp -r frontend/build /tmp/demo-app/frontend'
            }
        }
    }
    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build or deployment failed!'
        }
    }
}
