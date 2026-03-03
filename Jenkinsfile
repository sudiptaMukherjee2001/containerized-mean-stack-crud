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
        stage("Login to docker hub"){
            steps{
                withCredentials([usernamePassword(credentialsId: '22b95ae6-c01c-4793-b12b-81ecfc1518ad', passwordVariable: 'DOCKER_ACCESS_TOKEN', usernameVariable: 'DOCKER_USERNAME')]) {
                    sh "echo $DOCKER_ACCESS_TOKEN | docker login -u $DOCKER_USERNAME --password-stdin"
                }
            }
                post{
                    success{
                        echo "========Login to docker hub successfully========"
                    }
                    failure{
                        echo "========Login to docker hub execution failed========"
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
        stage("ssh to the vm and pull the images"){
            steps{

                sshagent(['6d75cf85-fa78-4e86-89cc-b433e22f0c6e']) {
                    sh "ssh -o StrictHostKeyChecking=no ec2-user@18.224.63.144 'ls -la; echo \\"Connected successfully\\"; whoami'"
                }
                echo "========Pulling the images from docker hub========"
                    // sh "docker pull sudipta4docker/dd_internship:frontend"
                    // sh "docker pull sudipta4docker/dd_internship:backend"                   
                
            }
            post{
                success{
                    echo "========ssh to the vm executed successfully========"
                }
                failure{
                    echo "========ssh to the vm execution failed========"
                }
        }
    }
    
}
}