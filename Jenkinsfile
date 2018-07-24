def podLabel = "edworker-${UUID.randomUUID()}"
properties([
  parameters([
    string(name: 'REPOSITORY', defaultValue: 'edyablo/demo-dotnet', description: 'Name of repository'),
    string(name: 'TEST_PROJECT', defaultValue: 'Demo.Test', description: 'Name of test project'),
    choice(name: 'CONFIGURATION', defaultValue: 'Debug', choices: ['Debug', 'Release'].join('\n'), description: 'Build configuration'),
  ])
])
dotnetTemplate(podLabel) {
  node(podLabel) {
    stage('checkout') {
      git url: "https://github.com/${params.REPOSITORY}.git"
    }
    stage('test') {
      container('dotnet') {
        sh """
          projects=`find . -regex '.*\\.Test\\.csproj'`
          for project in \$projects
          do
            dotnet test \$project --configuration ${params.CONFIGURATION}
          done
        """
      }
    }
  }
}
