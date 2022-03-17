pipeline {
    agent any
 
    stages {
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/poornima4824/KotlinDagger-1.git']]])
            }
        }
        stage('gradle clean') {
            steps {
                sh './gradlew clean'
            }
        }
        stage('build gradlew') {
            steps {
                sh './gradlew assembleRelease'
            }
        }
        stage('apk file') {
            steps {
                 archiveArtifacts artifacts: '**/*.apk', fingerprint: true, onlyIfSuccessful: true
            }
        }
        stage('Deploy') {
           steps {
               appCenter apiToken: 'c0e58abf7f9ff3ea91da3b3572f49a81ad89edbc',
                        ownerName: 'nagapoornima',
                        appName: 'andriod',  
                        file: 'var/lib/jenkins/workspace/andr-pipeline/app/build/outputs/apk/release/app-release-unsigned.apk',
                        distributionGroups: 'andriod-group'
           }
       }
    }
}

