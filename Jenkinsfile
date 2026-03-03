pipeline{
    
        agent any
    
    stages{
        stage("Build the images"){
            steps{
                echo "========Creating the images========"
                sh "docker compose build --no-cache"
            }
            post{
                success{
                    echo "========Image build successfully========"
                    sh "docker images | grep dd_internship"

                }
                failure{
                    echo "========Build the images execution failed========"
                }
            }
        }
        
        stage("push the images to docker hub"){
            steps{
                

                    echo "========Pushing the images to docker hub========"
                    sh "docker push sudipta4docker/dd_internship:frontend"
                    sh "docker push sudipta4docker/dd_internship:backend"                   
                
            }
        }
    }
    
}