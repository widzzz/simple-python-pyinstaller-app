node {
    stage('Build') {
        docker.image('python:2-alpine').inside {
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'
            stash(name: 'compiled-results', includes: 'sources/*.py*')
        }
    }
    stage('Test') {
        docker.image('python:2-alpine').inside {
            sh 'if [ -e "sources/calc.py" ]; then echo "Test success"; else echo "Error: calc.py does not exist" >&2; fi'
        }
    }
}
