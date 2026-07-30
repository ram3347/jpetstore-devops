// pipeline {
//     agent any

//     stages {
//         stage('Checkout') {
//             steps {
//                 echo 'Code downloaded successfully!'
//             }
//         }
//     }
// }
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
                stage('Docker Build') {
            steps {
                sh 'docker build -f Dockerfile.tomcat -t jpetstore:1.0 .'
            }
        }
                stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                        docker login -u $DOCKER_USER -p $DOCKER_PASS
                        docker tag jpetstore:1.0 $DOCKER_USER/jpetstore:1.0
                        docker push $DOCKER_USER/jpetstore:1.0
                    '''
                }
            }
                }

                stage('SSH to EC2') {
    steps {
        sshagent(['ec2-ssh']) {
            sh '''
                ssh -o StrictHostKeyChecking=no ec2-user@13.127.93.10 "hostname"
            '''
        }
    }
}
    }
}

// stage('SSH to EC2') {
//     steps {
//         sshagent(['ec2-ssh']) {
//             sh '''
//                 ssh -o StrictHostKeyChecking=no ec2-user@3.108.62.130 "
//                     docker pull ramvasanthhh/jpetstore:1.0
//                     docker stop jpetstore || true
//                     docker rm jpetstore || true
//                     docker run -d --name jpetstore -p 8081:8080 ramvasanthhh/jpetstore:1.0
//                 "
//             '''
//         }
//     }
// }
//     }
// }
// stage('Maven Build') {
//     steps {
//         sh '''
//         java -version
//         mvn -version
//         '''
//     }
// }
//     }
// }
// stage('Debug Environment') {
//     steps {
//         sh '''
//         whoami
//         echo "PATH=$PATH"
//         which java
//         java -version
//         which mvn
//         mvn -version
//         '''
//     }
// }
//     }
// }

