pipeline{
    agent any
    tools{
        maven 'maven_home'
    }
    stages{
        stage ('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to tomcat server') {
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://192.168.241.128:8090/')], contextPath: null, war: '**/*.war'

            }
        }
    }
}
