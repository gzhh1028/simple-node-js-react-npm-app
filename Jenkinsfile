pipeline {
    agent any
    stages {
        stage('Deploy') {
            steps {
                sshPublisher(
                    publishers: [
                        sshPublisherDesc(
                            configName: "aliyun-s1",
                            transfers: [
                                sshTransfer(
                                    sourceFiles: "**",
                                    remoteDirectory: "node-app"
                                )
                            ],
                            execCommands: [
                                "cd /root/node-app",
                                "npm install",
                                "npm run build",
                                "echo 构建完成！"
                            ]
                        )
                    ]
                )
            }
        }
    }
}
