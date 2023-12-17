// withDockerContainer
// node {
//     withDockerContainer('python:3.12.1-alpine3.19') {
//         stage('Build') {
//             sh 'python -m py_compile sources/add2vals.py sources/calc.py'
//             stash name: 'compiled-results', includes: 'sources/*.py*'
//         }
//     }
//     withDockerContainer('qnib/pytest') {
//         stage('Test') {
//             sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py'
//         }
//         post {
//             always {
//                 junit 'test-reports/results.xml'
//             }
//         }
//     }
// }

// docker.image
// A
// node {
//     docker.image('python:3.12.1-alpine3.19').inside {
//         stage('Build') {
//             sh 'python -m py_compile sources/add2vals.py sources/calc.py'
//             stash name: 'compiled-results', includes: 'sources/*.py*'
//         }
//     }
//     docker.image('qnib/pytest').inside {
//         stage('Test') {
//             sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py'
//         }
//         post {
//             always {
//                 junit 'test-reports/results.xml'
//             }
//         }
//     }
// }

// B
node {
    checkout scm
    withDockerContainer('python:3.12.1-alpine3.19').inside {
        stage('Build') {
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'
        }
    }
    withDockerContainer('qnib/pytest').inside {
        stage('Test') {
            sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py'
        }
    }
}

// gpt
// node {
//     stage('Build') {
//         docker.image('python:3.12.1-alpine3.19').inside {
//             sh 'python -m py_compile sources/add2vals.py sources/calc.py'
//             stash name: 'compiled-results', includes: 'sources/*.py*'
//         }
//     }
//     stage('Test') {
//         docker.image('qnib/pytest').inside {
//             sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py'
//         }
//         post {
//             always {
//                 junit 'test-reports/results.xml'
//             }
//         }
//     }
// }