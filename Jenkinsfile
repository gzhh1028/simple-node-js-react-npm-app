pipeline {
    agent any
    stages {
        stage('Deploy & Build on Remote Server') {
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
                                sshCommand(command: '''
                                    cd /root/node-app
                                    npm install
                                    npm run build
                                    echo "✅ 编译完成！"
                                ''')
                            ]
                        )
                    ]
                )
            }
        }
    }
}
