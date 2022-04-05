pipeline {
  environment {
        DOCKERHUB_CREDENTIALS=credentials('haleema-dockerhub')
    }
  agent none
  stages {
    stage('on-main') {
      when {
        branch 'main'
      }
      
          agent any
          steps {
            sh 'echo "edge1"'
            git branch: 'main', url: 'https://github.com/HaleemaEssa/jenkins-edge1.git'
            //sh 'docker build -t haleema/docker-edge1:latest .'
            sh 'docker run -v "${PWD}:/data" -t haleema/docker-edge1'

          }
        
         
        
          agent {label 'linuxslave1'}
          steps {
            sh 'echo "rpi" '
            git branch: 'main', url: 'https://github.com/HaleemaEssa/first_jenkins_project.git'
            //sh 'docker build -t haleema/docker-rpi:latest .'
            sh 'docker run --privileged -t haleema/docker-rpi'
          }
       
      }
   
        stage('on-devop') {
      when {
        branch 'main-devops'
      }
      
          agent any
          steps {
            sh 'echo "edge2"'
            git branch: 'main', url: 'https://github.com/HaleemaEssa/jenkins-edge2.git'
            //sh 'docker stop  a56987f86712; docker rm  a56987f86712'
            sh 'docker build -t haleema/docker-edge2:latest .'
            sh 'docker run -v "${PWD}:/data" -t haleema/docker-edge2'
          }
    
    
      agent {label 'aws'}
          steps {
            sh 'echo "cloud" '
            git branch: 'main', url: 'https://github.com/HaleemaEssa/jenkins-cloud.git'
           // sh 'docker build -t haleema/docker-cloud:latest .'
            sh 'docker run -v "${PWD}:/data" -t haleema/docker-cloud'
          }
    
      }
    }
}
   
