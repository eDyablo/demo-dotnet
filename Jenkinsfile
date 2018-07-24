@Library('ed-shared-lib@use-sh-resource-env')_

def podLabel = "edworker-${UUID.randomUUID()}"
properties([
  parameters([
    string(name: 'REPOSITORY', defaultValue: 'edyablo/demo-dotnet', description: 'Name of repository'),
    choice(name: 'BUILD_CONFIGURATION', defaultValue: 'Debug', choices: ['Debug', 'Release'].join('\n'), description: 'Build configuration'),
  ])
])
dotnetTemplate(podLabel) {
  node(podLabel) {
    stage('checkout') {
      git url: "https://github.com/${params.REPOSITORY}.git"
    }
    stage('test') {
      container('dotnet') {
        sh(libraryResource('dotnet-test.sh'))
      }
    }
  }
}
