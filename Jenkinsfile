// Jenkinsfiel Hemmder Alvarez Course
pipeline {
    agent any

    stages{
        stage("checkout"){
            steps{
                git branch:'main', url:'https://github.com/hemmder/course3-jenkins-gs-spring-petclinic'
            }
        }

        stage("build"){
            steps{
                sh "./mvnw package"
            }
        }

        stage("unit-testing"){
            steps{
                junit '**/target/surefire-reports/TEST*.xml'
                jacoco()
            }
        }
        
        stage("capture"){
            steps{
                archiveArtifacts artifacts: 'target/*.jar'
            }
        }
    }

    post{
        always{
                emailext body: "${env.BUILD_URL}\n${currentBuild.absoluteUrl}",
                    to: 'always@foo.bar', 
                    recipientProviders: [previous()],
                    subject: "${currentBuild.currentResult}: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]"
        }
    }

}