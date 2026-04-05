stage('Deploy') {
    steps {
        sshPublisher(publishers: [
            sshPublisherDesc(
                configName: 'aliyun-s1',
                transfers: [
                    sshTransfer(
                        sourceFiles: 'target/*.jar,Dockerfile',
                        remoteDirectory: 'hello-maven'
                    )
                ],
                // 👇 👇 👇 正确格式！没有警告，能正常远程执行！
                execCommands: [
                    sshCommand(command: '''
                        cd /home/jenkins/workspace/hello-maven
                        docker stop hellomaven || true
                        docker rm hellomaven || true
                        docker rmi nzc/hellomaven:1.0 || true
                        docker build -t nzc/hellomaven:1.0 .
                        docker run -d -p 880:8080 --name hellomaven nzc/hellomaven:1.0
                        echo "✅ 部署成功！端口：880"
                    ''')
                ]
            )
        ])
    }
}
