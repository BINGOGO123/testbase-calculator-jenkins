pipeline {
    agent any

    stages {
        stage('clean') {
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
        stage('package') {
            steps {
                powershell 'Compress-Archive -Path .\\testpackage\\* -DestinationPath .\\target.zip'
            }
        }
        stage('onboard') {
            steps {
                testBase useConfigurationFile: true, configurationFilePath: 'TestBase.json', credentialsId: 'dfclientsecret'
            }
        }
    }
}