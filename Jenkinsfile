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

//         stage('Maven Build') {
//             steps {
//                 sh 'mvn clean package'
//             }
//         }
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
stage('Debug Environment') {
    steps {
        sh '''
        whoami
        echo "PATH=$PATH"
        which java
        java -version
        which mvn
        mvn -version
        '''
    }
}
    }
}

