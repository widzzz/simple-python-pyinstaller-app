node {
    stage('Build') {
        docker.image('python:2-alpine').inside {
            // Copy the required files into the Docker container
            sh 'cp -r $WORKSPACE/sources .'

            // Perform the compilation
            sh 'echo $(pwd)'
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'

            // Stash the compiled results
            stash(name: 'compiled-results', includes: 'sources/*.py*')
        }
    }

    stage('Test') {
        docker.image('python:2-alpine').inside {
            // Retrieve the stashed files
            unstash('compiled-results')

            // Perform the test
            sh 'if [ -e "sources/calc.py" ]; then echo "Test success"; else echo "Error: calc.py does not exist" >&2; fi'
        }
    }
}
