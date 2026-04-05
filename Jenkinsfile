pipeline {
    agent any
    stages {
        stage('Install') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
        // 前端项目不需要 Docker 构建！
        // 只需要上传 dist/ 或 build/ 文件夹
        stage('Deploy') {
            steps {
                sshPublisher(
                    publishers: [
                        sshPublisherDesc(
                            configName: 'aliyun-s1',
                            transfers: [
                                sshTransfer(
                                    sourceFiles: 'build/**,dist/**', // 前端打包产物
                                    remoteDirectory: 'node-app'
                                )
                            ]
                        )
                    ]
                )
            }
        }
    }
}
