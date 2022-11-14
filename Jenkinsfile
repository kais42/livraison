pipeline {
   agent any
   stages {
    stage('Checkout') {
      steps {
        script {
           git branch: 'kais', 
           url: 'https://github.com/kais42/livraison.git'
          }
       }
    }
    stage('Build') {
      steps {
        script {
           sh 'ansible-playbook ansible/build.yml -i ansible/inventory/hosts.yml'
          }
       }
    }

    stage('Docker Build') {
      steps {
        script {
           sh 'ansible-playbook ansible/docker.yml -i ansible/inventory/hosts.yml'
          }
       }
    }
    stage('Pushing DockerHub') {
      steps {
        script {
           sh 'ansible-playbook ansible/docker-registry.yml -i ansible/inventory/hosts.yml'
          }
       }
    }

    stage('Monitoring') {
      steps {
        script {
           sh 'cd /var/lib/jenkins/workspace/livraison'
           sh 'docker-compose up -d'
          }
       }
    }
   }
}