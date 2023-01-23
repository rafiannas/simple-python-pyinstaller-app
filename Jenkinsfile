node {
    stage('Build'){
        agent {
            
            docker {
                image 'python:2-alpine'
            }  sh 'python -m py_compile sources/add2vals.py sources/calc.py'
            
        }
    }
    stage('Test'){
        agent {
            docker {
                image 'qnib/pytest'
            } sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
        
            post {
                always {
                     junit 'test-reports/results.xml'
                }
            }
        }
    }
    stage("Deploy"){
        agent {
            docker {
                  image 'cdrx/pyinstaller-linux:python2'
            }  sh 'pyinstaller --onefile sources/add2vals.py'

            post {
                success {
                    archiveArtifacts 'dist/add2vals'
                }
            }
        }
    }
    stage("Wait")
    {
        sh 'sleep 60'
    }
}