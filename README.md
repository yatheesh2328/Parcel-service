# mvn clean install 
# mvn spring-boot:run

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    def mvnHome = tool 'Maven'
                    def mvnCMD = "${mvnHome}/bin/mvn"

                    sh "${mvnCMD} clean install"
                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    def serverUrl = "<Your_Tomcat_Manager_URL>"
                    def username = "<Your_Tomcat_Username>"
                    def password = "<Your_Tomcat_Password>"
                    def warFileName = "<Your_WAR_File_Name>"

                    sh "curl -v --user ${username}:${password} --upload-file target/${warFileName} ${serverUrl}/manager/text/deploy?path=/${warFileName}"
                }
            }
        }
    }

    post {
        success {
            echo "Deployment to Tomcat successful!"
        }
        failure {
            echo "Deployment to Tomcat failed!"
        }
    }
}
