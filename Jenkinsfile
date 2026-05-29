// @Library("SharedLib") _
// pipeline{
//     agent {label "vinod"}
    
//     stages{
//         stage("clone"){
//             steps{
//                 script{
//                     clone("https://github.com/ajaykushwaha0508/jenkins-learning.git" ,"main")
//                 }
//             }
//         }
//          stage("build"){
//             steps{
//               script{
//                   docker_build("jenkins-vite" ,"latest")
//               }
//             }
//         }
//          stage("push on dockerHub"){
//             steps{
//             echo "Start pushing on docker hub"
//             script{
//                 dockerHub_push("jenkins-vite" ,"latest")
//             }
//             echo "pushed on docker hub"
//             }
            
//         }
//          stage("build && deploy"){
//             steps{
//             echo " Start deploying image on EC2"
//             script{
//                 dockerCompose_up()
//             }
//             echo " Image deployed successfully"
//             }
//         }
//         stage("cleaning previous images"){
//             steps{
//             echo " Start removing "
//             sh "docker image prune -a -f"
//             echo " Image removed successfully"
//             }
//         }
//     }
// }


// this code change is for my revising 
pipeline {

    agent any


    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/ajaykushwaha0508/jenkins-learning.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build Project') {
            steps {
                bat 'npm run build'
            }
        }

       stage('docker build'){
               steps{
                echo "this is building image in docker"
                bat "docker build -t react-app:latest ."
               }
        }

        stage('docker deploy'){
               steps {
                bat 'docker stop react-app-con || exit 0'
                bat 'docker rm react-app-con || exit 0'
                bat 'docker run -d -p 6000:9000 --name react-app-con react-app'
            }
        }



    }

    post {

        success {
            echo 'Build Successfully  Done🚀'
        }

        failure {
            echo 'Build Failed ❌'
        }

    }
}
