node {
    stage('Build'){
        agent {
            
            docker {
                sh 'echo "Build Process"'
                image 'python:2-alpine'
            }  sh 'python -m py_compile sources/add2vals.py sources/calc.py'
            
        }
    }
    stage('Test'){
        agent {
            docker {
                sh 'echo "Test Process"'
                image 'qnib/pytest'
            } sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
        
            post {
                always {
                     junit 'test-reports/results.xml'
                }
            }
        }
    }
    stage("Manual Approval")
    {
        sh 'echo "Approval Process"'
        input "Lanjutkan ke tahap Deploy?"
    }
    stage("Deploy"){
        agent {
            docker {
                  sh 'echo "Deploy Process"'
                  image 'cdrx/pyinstaller-linux:python2'
            }  sh 'pyinstaller --onefile sources/add2vals.py'

            post {
                success {
                    archiveArtifacts 'dist/add2vals'
                }
            }
        }
    }
    stage("Waiting")
    {
        sh 'sleep 60'
    }
}