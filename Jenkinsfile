pipeline {
    agent any
    stages
    {
        stage('Build Docker Image') {
            steps {
                echo "Build Docker Image"
                sh "docker build -t kubdemoapp:v1 ."
            }
        }
        stage('Docker Login') {
            steps {
                  sh 'docker login -u shreyachundi -p Karthikeya@011'
                }
            }
        stage('push Docker Image to Docker Hub') {
            steps {
                echo "push Docker Image to Docker Hub"
                sh "docker tag kubdemoapp:v1 shreyachundi/week8_docker:week9image"               
                    
                sh "docker push shreyachundi/week8_docker:week9image"
                
            }
        }
        stage('Deploy to Kubernetes') { 
            steps { 
                    // apply deployment & service 
                    sh 'kubectl apply -f deployment.yaml --validate=false' 
                    sh 'kubectl apply -f service.yaml' 
            } 
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}