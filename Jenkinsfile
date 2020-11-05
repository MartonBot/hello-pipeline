pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/MartonBot/hello-pipeline']]])

                sh "dotnet build HelloApi --configuration Release"
            }

        }
    }
}
