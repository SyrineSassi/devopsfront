pipeline{
    agent any


    tools {
        maven 'M2_HOME'
    }


	stages {


 stage('Getting project from Git') {
            steps{
      			checkout([$class: 'GitSCM', branches: [[name: '*/Syrine']],
			extensions: [],
			userRemoteConfigs: [[url: 'https://github.com/SyrineSassi/devopsfront.git']]])
            }
        }


        stage('Cleaning the project') {
            steps{
                sh "npm install"
            }
        }





        stage('Artifact Construction') {
            steps{
                sh "ng build  "
            }
        }



stage('Build Docker Image') {
                      steps {
                          script {
                            sh 'docker build -t syrinesassi/angular-app:latest .'
                          }
                      }
                  }




                  stage('login dockerhub') {
                                        steps {
                                      sh 'echo dckr_pat_3cooqrMsOEE9QuUUuYU0OCQDGj4 | docker login -u syrinesassi --password Syrine1234'
                                            }
		  }





	                      stage('Push Docker Image') {
                                        steps {
                                   sh 'docker push syrinesassi/angular-app:latest'
                                            }
		  }



        stage('Run Angular Container') {
                      steps {
                          script {
                            sh 'docker-compose up -d'
                          }
                      }
                  }

}


}
