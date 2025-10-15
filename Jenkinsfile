pipeline {
  agent any
      
  stages {
    stage('Git Checkout') {
      steps {
        echo 'This stage is to clone the repo from github'
        git branch: 'master', url: 'https://github.com/sudharani123-del/star-agile-health-care.git'
                        }
            }
    stage('Create Package') {
      steps {
        echo 'This stage will compile, test, package my application'
        sh 'mvn package'
                          }
            }
    
  /* stage('Create Docker Image') {
      steps {
        echo 'This stage will Create a Docker image'
        sh 'docker build -t sudharani000/healthcare:1.0 .'
                          }
            }
     stage('Docker-Login') {
           steps {
              withCredentials([usernamePassword(credentialsId: 'dockercreds', passwordVariable: 'dockerpassword', usernameVariable: 'dockerlogin')]) {
               sh 'docker login -u ${dockerlogin} -p ${dockerpassword}'
    }
  }
 } 
    stage('Docker Push-Image') {
      steps {
        echo 'This stage will push my new image to the dockerhub'
        sh 'docker push sudharani000/healthcare:1.0'
            }
      } */
    stage('AWS-Login') {
      steps {
        withCredentials([aws(accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'awslogin', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
         }
      }
    }
     stage('setting the Kubernetes Cluster') {
      steps {
        dir('terraform_files'){
          sh 'terraform init'
          sh 'terraform validate'
          sh 'terraform apply --auto-approve'
          sh 'sleep 20'
             }
      }
    }
         stage('deploy kubernetes'){
steps {
        sh '''
          sudo chmod 600 ./terraform_files/newkeypair.pem
          
          if ! command -v minikube >/dev/null 2>&1; then
            echo "⚙️ Installing Minikube..."
            curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
            sudo install minikube-linux-amd64 /usr/local/bin/minikube
          fi
          
          minikube start
        '''
 stage('deploy kubernetes'){
    steps {
        sh '''
         sudo chmod 600 ./terraform_files/newkeypair.pem
         
        if ! command -v medicure >/dev/null 2>&1; then
          echo "Medicure not found, installing..."
          sudo apt-get update && sudo apt-get install -y medicure
        else
          echo "Medicure already installed."
        fi
        ''' 
    }
 }
    }
   }
  }
}

}
  
  
  

    

