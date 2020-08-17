def branchesName() {
  def branchName = "${env.BRANCH_NAME}"

  if (branchName == "sprint4") {
    return "sprint4"
  } else if (branchName == "dev") {
    return "dev"
  } else if (branchName == "qa") {
    return "qa"
  } else if (branchName == "master") {
    return "master"
  }
}
 pipeline {
  environment {
    branch = branchesName()
    CI = 'true'
    HOME = '.'
  }
  agent {
        docker {
            image 'node:6-alpine'
            args '-p 3000:3000'
        }
  }
  stages {

	stage('Unit test and Code Coverage') {
      /*when {
        anyOf {
          branch 'dev' ; branch 'qa' ; branch 'master';
        }
      }*/
    steps{
        script {
        // sh 'curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash'
         sh "echo ${branch} , ${env.BRANCH_NAME}"
         sh "echo ${env}"
		 sh 'npm install ; npm run test'
         }
      }
     }


   	/*stage('SonarQube Analysis') {
	    environment {
        scannerHome = tool 'SonarQubeScanner'
        }
      when {
        anyOf {
          branch 'sprint4' ; branch 'dev' ; branch 'qa' ; branch 'master' ; branch 'test-cases'
             }
            }
      steps{
        script {
          withSonarQubeEnv('sonarqube') {
		  sh 'source ~/.bashrc'
          sh '${scannerHome}/bin/sonar-scanner'
           }
         }
			 }
     }

    stage('Build and Tag Image') {
      when {
        anyOf {
          branch 'sprint4' ; branch 'dev' ; branch 'qa' ; branch 'master'
        }
      }
      steps{
        script {
          sh "docker build -t registry:5000/backend-${env.branch}:$BUILD_NUMBER --no-cache ."
          sh "docker tag registry:5000/backend-${env.branch}:$BUILD_NUMBER registry:5000/backend-${env.branch}:latest "
        }
      }
    }



    stage ('Push to Registry'){
      when {
        anyOf {
          branch 'sprint4' ; branch 'dev' ; branch 'qa' ; branch 'master'
        }
      }
      steps{
        script {
          sh "docker push registry:5000/backend-${env.branch}:$BUILD_NUMBER"
          sh "docker push registry:5000/backend-${env.branch}:latest"
        }
      }
    }

    stage ('Deploy to Environment') {
      when {
        anyOf {
          branch 'dev' ; branch 'qa' ; branch 'master'
        }
      }
      steps{
        script {
		     if (branch == "dev") {
               sh 'ssh -i ~/keys/PDM_DEV_QA.pem ec2-user@dev /home/ec2-user/stacks/backend/deploy.sh'
             }
		     if (branch == "qa") {
               sh 'ssh -i ~/keys/PDM_DEV_QA.pem ec2-user@qa /home/ec2-user/stacks/backend/deploy.sh'
             }
		}
      }
    }*/

  }
 }
