pipeline {
    agent {
        kubernetes {
            label 'kaniko'
        }
    }
    stages  {
      stage ('Build with Kaniko') {
       steps {
        git 'https://github.com/Sivajey/kaniko.git'
        container(name: 'kaniko', shell: '/busybox/sh') {
        withEnv(['PATH+EXTRA=/busybox:/kaniko']) {
          sh '''#!/busybox/sh
          /kaniko/executor -f `pwd`/Dockerfile -c `pwd` --destination=docker.io/sivajey/kaniko:v1
          '''
        }
        }
      }
    }
  }
}
