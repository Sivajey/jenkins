pipeline {
    agent {
        any {
            label 'kaniko'
            yaml """
apiVersion: v1
kind: Pod
metadata:
  name: kaniko
spec:
  containers:
  - name: jnlp
    image: jenkins/jnlp-slave:3.35-5-alpine
    resources:
      limits:
        cpu: 500m
        memory: 250Mi
      requests:
        cpu: 500m
        memory: 250Mi
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
    volumeMounts:
      - name: docker-config
        mountPath: /kaniko/.docker/
        """
        }
    }
    stages  {
      stage ('Build with Kaniko') {
       steps {
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
