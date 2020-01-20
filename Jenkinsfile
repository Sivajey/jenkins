pipeline {
    agent {
        kubernetes {
            label 'kaniko'
            yaml """
apiVersion: v1
kind: Pod
metadata:
  name: kaniko
spec:
  containers:
  - name: kaniko
    image: gcr.io/kaniko-project/executor:debug-v0.9.0
    command:
    - /busybox/cat
    resources:
      limits:
        cpu: 2
        memory: 2Gi
      requests:
        cpu: 0.5
        memory: 500Mi
    tty: true
        """
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
