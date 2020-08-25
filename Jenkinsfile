pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven-container"
    }

    stages {
        stage('verify') {
            steps {
                sh "mvn -v"
            }
        }
        stage('compile') {
            steps {
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('test') {
            steps {
                sh "mvn test"
            }
            post {
                success {
                    junit '**/target/surefire-reports/*.xml'
                    //slackSend channel: 'jenkins-training', color: '#00FF00', message: 'Succes (Antoine)', teamDomain: 'devinstitut', tokenCredentialId: 'slack-token'
                    //discordSend description: 'success - Antoine', footer: '', image: '', link: '', result: '', thumbnail: '', title: 'success', webhookURL: 'https://discordapp.com/api/webhooks/747819422705778738/dHWPHidlNLpiiKftWU84__Ss2LAkws77Swfdk5OWs22qla3hlI1B4zywW8ROg4nAwjRM'
                }
                failure {
                    sh "echo 'failure'"
                    //slackSend channel: 'jenkins-training', color: '#FF0000', message: 'Failure (Antoine)', teamDomain: 'devinstitut', tokenCredentialId: 'slack-token'
                }
            }
        }
    }
}
