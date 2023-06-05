node {
    stage('Build') {
        docker.image('python:2-alpine').inside {
            sh 'pwd'
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'
        }
    }
    
    stage('Test') {
    node {
        docker.image('qnib/pytest').inside {
            // Perform the test
            sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
            
            // Archive the test results
            archiveArtifacts 'test-reports/results.xml'
            
            // Publish the test results
            junit 'test-reports/results.xml'
        }
    }
}
