// 这是 声明式流水线 → 必须这样写！
pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Deploy') {
            steps {
                sshPublisher(
                    publishers: [
                        sshPublisherDesc(
                            configName: 'aliyun-s1',
                            transfers: [
                                sshTransfer(
                                    sourceFiles: 'target/*.jar,Dockerfile',
                                    remoteDirectory: 'hello-maven'
                                )
                            ],
                            execCommands: [
                                sshCommand(command: '''
                                    cd /home/jenkins/workspace/hello-maven
                                    docker stop hellomaven || true
                                    docker rm hellomaven || true
                                    docker rmi nzc/hellomaven:1.0 || true
                                    docker build -t nzc/hellomaven:1.0 .
                                    docker run -d -p 880:8080 --name hellomaven nzc/hellomaven:1.0
                                    echo "✅ 部署成功！"
                                ''')
                            ]
                        )
                    ]
                )
            }
        }
    }
}
