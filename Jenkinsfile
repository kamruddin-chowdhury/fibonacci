pipeline {
    agent any
    parameters {
        choice(name: 'NUMBER',
            choices: [10,20,30,40,50,60,70,80,90],
            description: 'Select the value for F(n) for the Fibonnai sequence.')
    }
    options {
        buildDiscarder(logRotator(daysToKeepStr: '10', numToKeepStr: '10'))
        timeout(time: 12, unit: 'HOURS')
        timestamps()
    }
    
    stages {
        stage('Make executable') {
            steps {
                sh('chmod +x ./scripts/fibonacci.sh')
            }
        }
        stage('Relative path') {
            steps {
                sh("./scripts/fibonacci.sh ${params.NUMBER}")
            }
        }
        stage('Full path') {
            steps {
                sh("${env.WORKSPACE}/scripts/fibonacci.sh ${params.NUMBER}")
            }
        }
        stage('Full path 2') {
            steps {
                sh("/var/lib/jenkins/workspace/fibonacci//scripts/fibonacci.sh ${params.NUMBER}")
            }
        }
        
        stage('Change directory') {
            steps {
                dir("${env.WORKSPACE}/scripts"){
                    sh("./fibonacci.sh ${env.NUMBER}")
                }
            }
        }
        
    }
}
