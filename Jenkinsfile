pipeline {
    agent any

    stages {
        stage('clean1') {
            steps {
                powershell 'rm testpackage/bin/calculator.msi -ErrorAction SilentlyContinue'
            }
        }
        stage('build') {
            steps {
                powershell '.\\build.ps1'
            }
        }
        stage('makeup') {
            steps {
                powershell 'mv windows_installer/calculator.msi testpackage/bin/'
            }
        }
        stage('clean2') {
            steps {
                powershell 'rm target.zip -ErrorAction SilentlyContinue'
            }
        }
        stage('package') {
            steps {
                powershell 'Compress-Archive -Path .\\testpackage\\* -DestinationPath .\\target.zip'
            }
        }
        stage('onboard') {
            steps {
                testBase useConfigurationFile: true, configurationFilePath: 'TestBase.json', credentialsId: 'prod-client-secret'
            }
        }
    }
}