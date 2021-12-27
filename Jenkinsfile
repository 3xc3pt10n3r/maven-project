pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: 'localhost', description: 'Staging Server')
    }

    // triggers {
    //      pollSCM('* * * * *')
    //  }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
                sh 'docker build . -t tomcatwebapp:{env.BUILD_ID}'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        // stage ('Deployments'){
        //     parallel{
        //         stage ('Deploy to Staging'){
        //             steps {
        //                 sh "curl http://tomcat:tomcat123@localhost:8090/manager/text/undeploy?path=/webapp"
        //                 sh "curl --upload-file webapp/target/webapp.war http://tomcat:tomcat123@localhost:8090/manager/text/deploy?path=/webapp&update=true"
        //             }
        //         }
        //     }
        // }
    }
}