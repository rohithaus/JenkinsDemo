pipeline {
  agent any
  stages {
    stage("Cleanup workspace"){
      steps{
        cleanWs()
      }
    }
    stage('Checkout') {
      steps {
        sh 'echo passed'
        git branch: 'main', url: 'https://github.com/rohithaus/JenkinsDemo.git'
      }
    }
    stage('Build and Test') {
      steps {
        sh 'ls -ltr'
        // build the project and create a JAR file
      }
    }
    stage('Update Deployment File') {
        environment {
            GIT_REPO_NAME = "JenkinsDemo"
            GIT_USER_NAME = "rohithaus"
        }
        steps {
            withCredentials([string(credentialsId: 'github', variable: 'GITHUB_TOKEN')]) {
                sh '''
                    git config user.email "rohithrockr@gmail.com"
                    git config user.name "Rohith Katikaneni"
                    sed -i "s/replaceImageTag/22/g" sample-repo/manifests/deployment.yml
                    git add sample-repo/manifests/deployment.yml
                    git commit -m "Update deployment image to 22"
                    git push https://${GITHUB_TOKEN}@github.com/${GIT_USER_NAME}/${GIT_REPO_NAME} HEAD:main
                '''
            }
        }
    }
  }
}
