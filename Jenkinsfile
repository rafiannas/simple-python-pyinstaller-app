Node {
    stage('Build'){
        agent {
            docker {
                image 'python:2-alpine'
            }
        }
    }
    stage('Test'){
        agent {
            docker {
                image 'qnib/pytest'
            }
        }
    }
}