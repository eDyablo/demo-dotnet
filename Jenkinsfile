def podLabel = "edworker-${UUID.randomUUID()}"
dotnetTemplate(podLabel) {
    node(podLabel) {
        stage('checkout') {
            git url: 'https://github.com/eDyablo/demo-dotnet.git'
        }
        stage('test') {
            container('dotnet') {
                sh 'dotnet test Demo.Test'
            }
        }
    }
}
