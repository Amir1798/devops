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



<<<<<<< HEAD

=======
         
>>>>>>> 2a8c49ea57e5a14a10ad0cd942dd570bad406811
        stage('SONARQUBE') {
            steps{

             	sh "mvn clean verify sonar:sonar -Dsonar.projectKey=devops -Dsonar.projectName='devops' -Dsonar.host.url=http://172.10.0.140:9000 -Dsonar.token=sqp_f9d5c0e7497edcecee9f583d39d1fa85e64eb904 "
            }
        }


        stage('Publish to Nexus') {
            steps {


  sh 'mvn deploy'


            }
        }

    }
<<<<<<< HEAD
}
=======
}

>>>>>>> 2a8c49ea57e5a14a10ad0cd942dd570bad406811
