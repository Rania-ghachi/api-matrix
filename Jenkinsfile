pipeline {
    agent any

    stages {

        stage('test') {

                    steps {
                           bat 'C://apache-maven-3.9.12//bin//mvn test'
                           junit 'target/surefire-reports/*.xml'
                           cucumber reportTitle: 'API Report',
                                  fileIncludePattern: 'target/example-report.json'
                           recordCoverage(tools: [[parser: 'JACOCO']],
                                   id: 'jacoco', name: 'JaCoCo Coverage',
                                   sourceCodeRetention: 'EVERY_BUILD',
                                   qualityGates: [
                                           [threshold: 60.0, metric: 'LINE', baseline: 'PROJECT', unstable: true],
                                           [threshold: 60.0, metric: 'BRANCH', baseline: 'PROJECT', unstable: true]])


                          }


                }
/*         stage('archivage') {
                    steps {

                        bat '''
                        mvn javadoc:javadoc
                        mkdir doc
                        xcopy target\\site\\* doc\\ /E /I /Y
                        powershell Compress-Archive -Path doc\\* -DestinationPath doc.zip -Force
                        '''
                        archiveArtifacts 'doc.zip'

                        publishHTML(target: [
                            allowMissing: false,
                            alwaysLinkToLastBuild: true,
                            keepAll: true,
                            reportDir: 'target/site/apidocs',
                            reportFiles: 'index.html',
                            reportName: 'Documentation'
                        ])
                    }
        } */

         stage('build') {
            steps {
                bat 'C://apache-maven-3.9.12//bin//mvn package'
                archiveArtifacts 'target/*.jar'
            }
            /* post {
                failure {
                    mail(
                        subject: "Build echec",
                        body: "Le build a echoue",
                        to: "assia.cntsid@gmail.com"
                    )
                }
                success {
                    mail(
                        subject: "Build reussi",
                        body: "Le build a reussi",
                        to: "assia.cntsid@gmail.com"
                    )
                } */

        }

          /*stage('documentation') {
            steps {
                bat '''
                if not exist doc mkdir doc
                xcopy target\\site\\* doc\\ /E /I /Y
                powershell Compress-Archive -Path doc\\* -DestinationPath doc.zip
                '''
                archiveArtifacts 'doc.zip'

                publishHTML(target: [
                    allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'target/site/jacoco',
                    reportFiles: 'index.html',
                    reportName: 'Documentation'
                ])
            }
        } /*


           stage('parallel') {
                          parallel {
                            stage('Unit Testing1') {
                                steps {
                                          bat 'mvn javadoc:javadoc'
                                                publishHTML(target: [
                                                    allowMissing: false,
                                                    alwaysLinkToLastBuild: true,
                                                    keepAll: true,
                                                    reportDir: 'target/site/apidocs',
                                                    reportFiles: 'index.html',
                                                    reportName: 'Documentation'
                                                ])
                                            }
                            }
                            stage('Unit Testing2') {
                                steps {
                                                bat 'mvn test'

                                       }
                            }
                          }
                }



*/

         stage('deploy') {
            when {
                branch 'master'
                  }
            steps {
                   //bat 'docker-compose up --build -d'
                   bat 'mvn deploy'
                    //archiveArtifacts 'target *//*  *//*.jar'
                    //coment
                  }
            /* post {
                            failure {
                                mail(
                                    subject: "Build echec",
                                    body: "Le build a echoue",
                                    to: "assia.cntsid@gmail.com"
                                )
                            }
                            success {
                                mail(
                                    subject: "Build reussi",
                                    body: "Le build a reussi",
                                    to: "assia.cntsid@gmail.com"
                                )
                            }
                            */

        }

        stage('slack') {

                    steps {
                           //bat 'docker-compose up --build -d'
                           bat '''curl -X POST -H 'Content-type: application/json' --data '{"text":"Hello, World!"}'
                           "$slack_webhook"'''

                          }

                }


    }
}
