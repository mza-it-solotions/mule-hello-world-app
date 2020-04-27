pipeline {

  agent any
  environment {
    //adding a comment for the commit test
    DEPLOY_CREDS = credentials('deploy-anypoint-user')
    MULE_VERSION = '4.2.2'
    BG = "MZA"
    WORKER = "MICRO"
  }
  stages {
    stage('Build') {
      steps {
            bat 'mvn -B -U -e -V clean -DskipTests package'
      }
    }

    stage('Test') {
      steps {
          bat "mvn test"
      }
    }

     stage('Deploy Development') {
      environment {
        ENVIRONMENT = 'Sandbox'
        APP_NAME = 'dev-mule-hello-world-app'
      }
      steps {
            bat 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version="4.2.2" -Danypoint.username="MZAM4B7" -Danypoint.password="Raz10zaq" -Dcloudhub.app="dev-mule-hello-world-app" -Dcloudhub.environment="Sandbox" -Dcloudhub.bg="MZA" -Dcloudhub.worker.type="MICRO" -Dcloudhub.workers="1" -Pdev'
      }
    }
  }
}