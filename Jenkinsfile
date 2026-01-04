@Library("SharedLib") _
pipeline{
    agent {label "vinod"}
    
    stages{
        stage("clone"){
            steps{
                script{
                    clone("https://github.com/ajaykushwaha0508/jenkins-learning.git" ,"main")
                }
            }
        }
         stage("build"){
            steps{
              script{
                  docker_build("jenkins-vite" ,"latest")
              }
            }
        }
         stage("push on dockerHub"){
            steps{
            echo "Start pushing on docker hub"
            script{
                dockerHub_push("jenkins-vite" ,"latest")
            }
            echo "pushed on docker hub"
            }
            
        }
         stage("build && deploy"){
            steps{
            echo " Start deploying image on EC2"
            script{
                dockerCompose_up()
            }
            echo " Image deployed successfully"
            }
        }
        stage("cleaning previous images"){
            steps{
            echo " Start removing "
            sh "docker image prune -a -f"
            echo " Image removed successfully"
            }
        }
    }
}
