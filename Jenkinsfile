pipeline {
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }

    triggers {
        cron('*/5 * * * *')
    }

    agent {
        kubernetes {
            yaml """
apiVersion: v1
kind: Pod
metadata:
spec:
  containers:
  - name: busybox
    image: busybox:latest
    command:
    - cat
    tty: true
"""
        }
    }

    environment {
        TWISTLOCK = credentials('twistlock')
    }

    stages {
        stage('Build') {
            steps {
                container('busybox') {
                    sh "echo Fetched secret is: ${env.TWISTLOCK}"
                }
            }
        }
    }
}
