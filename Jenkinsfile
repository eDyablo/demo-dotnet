def podLabel = "edworker-${UUID.randomUUID()}"
podTemplate(
    cloud: 'kubernetes-dev',
    namespace: 'jenkins',
    label: podLabel,
    containers: [
        containerTemplate(
            name: 'dotnet',
            image: 'microsoft/dotnet',
            ttyEnabled: true,
            command: 'cat')
    ]
    ) {
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
