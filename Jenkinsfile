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
    }
}
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

