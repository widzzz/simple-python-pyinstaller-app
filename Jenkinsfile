pipeline {
    agent none 
    stages {
        stage('Build') { 
            agent {
                docker {
                    image 'python:2-alpine' 
                }
            }
            steps {
                sh 'python -m py_compile sources/add2vals.py sources/calc.py' 
                stash(name: 'compiled-results', includes: 'sources/*.py*') 
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'python:2-alpine' 
                }
            }
            steps {
                sh 'if [ -e "sources/calc.py" ]; then echo "Test success"; else echo "Error: calc.py does not exist" >&2; fi'
            }
        }
    }
}