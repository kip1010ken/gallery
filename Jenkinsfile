def COLOR_MAP = [
    'SUCCESS': 'good', 
    'FAILURE': 'danger',
]

pipeline {
    agent any

    environment{
        RENDER_DEPLOY_HOOK = credentials('RENDER_DEPLOY_HOOK')
    }

    tools{
        nodejs 'node23'
    }

    stages{
        stage("fetch code from git"){
            steps{
                git branch:'master', url: 'https://github.com/kip1010ken/gallery.git'

            }
        }

        stage("install depencies"){
            steps{
                sh 'npm install'
            }
        }

        stage ("unit test"){
            steps{
                sh 'npm test'
            }
        }

        stage('deploy to render'){
            steps{
                script {
                    sh "curl -X POST ${RENDER_DEPLOY_HOOK}"
                }
            }
        }
    }
    post {

        always {
            slackSend(channel: '#kenneth_ip1',
            color: COLOR_MAP[currentBuild.currentResult],
            message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} \n More info at: ${env.BUILD_URL}")
        }
        
        
    }


}