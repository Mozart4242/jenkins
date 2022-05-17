pipeline {
  agent any
  stages {
    stage('Checkout Source') {
      steps {
        git(url: 'https://github.com/mozart4242/jenkins.git', branch: 'main')
      }
    }

    stage('Build image') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }

      }
    }

    stage('Push Image') {
      steps {
        script {
          docker.withRegistry( "" ) {
            dockerImage.push()
          }
        }

      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig")
        }

      }
    }

  }
  environment {
    registry = '10.132.132.104:5000/mozart4242/myweb'
    dockerImage = ''
  }
}
