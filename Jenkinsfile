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
                    image 'qnib/pytest' 
                }
            }
            steps {
                sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py' 
            }
            post {
                always {
                    junit 'test-reports/results.xml' 
                }
            }
        }

        stage('Manual Approval') {
            steps {
                input "Please approve to proceed with deployment"
            }
        }
    }
}

// node {
//     checkout scm
//     docker.image('python:3.12.1-alpine3.19').inside {
//         stage('Build') {
//             sh 'python -m py_compile sources/add2vals.py sources/calc.py'
//         }
//     }
//     docker.image('qnib/pytest').inside {
//         stage('Test') {
//             sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py'
//         }
//     }
//     stage('Manual Approval') {
//         input message: 'Lanjutkan ke tahap Deploy?'
//     }
//     stage('Deploy') {
//         withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
//             sh 'docker build -t 890890123890/simple-python-app .'
//             sh "echo $PASS | docker login -u $USER --password-stdin"
//             sh 'docker push 890890123890/simple-python-app'
//         }
        
//         sshagent(['ec2-app']) {
//             def cmd = 'sudo docker pull 890890123890/simple-python-app:latest && sudo docker run --name app -d 890890123890/simple-python-app:latest'
//             sh "ssh -o StrictHostKeyChecking=no ubuntu@18.136.105.164 '${cmd}'"
//         }

//         sleep 60

//         sshagent(['ec2-app']) {
//             def cmd = 'sudo docker rm app'
//             sh "ssh -o StrictHostKeyChecking=no ubuntu@18.136.105.164 ${cmd}"
//         }
//     }
// }

// node {
//     checkout scm
//     stage('Build') {
//         docker.image('python:2-alpine').inside {
//             sh 'python -m py_compile sources/add2vals.py sources/calc.py'
//         }
//     }
    
//     stage('Test') {
//         docker.image('qnib/pytest').inside {
//             sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
//         }
//     }

//     stage('Manual Approval') {
//         input message: 'Lanjutkan ke tahap Deploy?'
//     }

//     stage('Deploy') {
//         withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
//             sh 'docker build -t 890890123890/simple-python-app .'
//             sh "echo $PASS | docker login -u $USER --password-stdin"
//             sh 'docker push 890890123890/simple-python-app'
//         }
        
//         sshagent(['ec2-app']) {
//             def cmd = 'sudo docker pull 890890123890/simple-python-app:latest && sudo docker run --name app -d 890890123890/simple-python-app:latest'
//             sh "ssh -o StrictHostKeyChecking=no ubuntu@18.136.105.164 '${cmd}'"
//         }

//         sleep 60

//         sshagent(['ec2-app']) {
//             def cmd = 'sudo docker rm app'
//             sh "ssh -o StrictHostKeyChecking=no ubuntu@18.136.105.164 ${cmd}"
//         }
//     }
// }