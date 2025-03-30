pipeline {
    agent any

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
    }


}