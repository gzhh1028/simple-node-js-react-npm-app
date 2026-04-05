pipeline {
    agent any
    stages {
        // 只上传代码！不做任何构建！
        stage('Deploy to Server') {
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
                            ]
                        )
                    ]
                )
            }
        }
    }
}
