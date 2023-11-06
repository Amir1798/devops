pipeline{
    agent any



    stages {


        stage('Getting project from Git') {
            steps{
      			checkout([$class: 'GitSCM', branches: [[name: '*/main']],
			extensions: [],
			userRemoteConfigs: [[url: 'https://github.com/Amir1798/devops.git']]])
            }
        }


       stage('Cleaning the project') {
            steps{
                	sh "mvn -B -DskipTests clean  "
            }
        }



        stage('Artifact Construction') {
            steps{
                	sh "mvn -B -DskipTests package "
            }
        }



         
        stage('SONARQUBE') {
            steps{

             		mvn clean verify sonar:sonar -Dsonar.projectKey=devops -Dsonar.projectName='devops' -Dsonar.host.url=http://172.10.0.140:9000 -Dsonar.token=sqp_f9d5c0e7497edcecee9f583d39d1fa85e64eb904
            }
        }


        stage('Publish to Nexus') {
            steps {


  sh 'mvn deploy'


            }
        }

stage('Build Docker Image') {
                      steps {
                          script {
                            sh 'docker build -t toumi15/spring-app:Toumi .'
                          }
                      }
                  }

                  stage('login dockerhub') {
                                        steps {
                                     // sh 'echo dckr_pat_-SnwrdC_ELsL6it2JT6cgIcAlrs | docker login -u azizbenhaha --password-stdin'
				sh 'docker login -u toumi15 --password dckr_pat_0iaom9peVjYUg0VIvUkeT-5V4bg'
                                            }
		  }

	                      stage('Push Docker Image') {
                                        steps {
                                   sh 'docker push toumi15/spring-app:Toumi'
                                            }
		  }









}


    /*    post {
		success{
		mail bcc: '', body: '''Dear Houssem Toumi,
we are happy to inform you that your pipeline build was successful.
Great work !
-Jenkins Team-''', cc: '', from: 'houssem.toumi@@esprit.tn', replyTo: '', subject: 'Build Finished - Success', to: 'houssem.toumi@@esprit.tn'
		}

		failure{
mail bcc: '', body: '''Dear  Houssem Toumi,
we are sorry to inform you that your pipeline build failed.
Keep working !
-Jenkins Team-''', cc: '', from: 'houssem.toumi@@esprit.tn', replyTo: '', subject: 'Build Finished - Failure', to: 'houssem.toumi@@esprit.tn'
		}

       always {
		emailext attachLog: true, body: '', subject: 'Build finished',from: 'houssem.toumi@@esprit.tn' , to: 'houssem.toumi@@esprit.tn'
            cleanWs()
       }
    }

*/

}

