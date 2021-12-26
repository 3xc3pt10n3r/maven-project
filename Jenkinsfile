pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archieving ...'
                    archieveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('Deploy to Staging ...') {
            steps {
                echo 'Deploying....'
                build job: 'deploy-staging-maven-project'
            }
        }
    }
}
