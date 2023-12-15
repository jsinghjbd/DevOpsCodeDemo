pipeline{
    tools{
        maven 'Jenkins-Maven'
    }
agent{
    label 'workervm'
}
stages{
    stage('1. CloneGitRepo'){
        parallel{
             stage('GitCloneMasterVM'){
                 agent {
                     label 'mastervm'
                 }
                steps{
                    sh 'echo "Hostname: `hostname` Date: `date`"'
                    git 'https://github.com/Sonal0409/DevOpsCodeDemo.git'
                }
            }
            stage('GitCloneWorkerVM'){
                 agent {
                     label 'workervm'
                 }
                steps{
                    sh 'echo "Hostname: `hostname` Date: `date`"'
                    git 'https://github.com/Sonal0409/DevOpsCodeDemo.git'
                }
            }
        }
    }
    stage('Parallel Stages')
    {
        parallel{
             stage('2. BuildCode'){
                 agent {
                     label 'mastervm'
                 }
                steps{
                    sh 'sleep 15'
                    sh 'echo "`hostname`"'
                    sh 'mvn compile'
                    
                }
            }
            stage('3. ReviewCode'){
                agent {
                     label 'workervm'
                 }
                steps{
                    sh 'sleep 15'
                    sh 'echo "`hostname`"'
                    sh 'mvn pmd:pmd'
                    
                }
            }
        }
    }
    stage('4. ExecuteTestCases'){
        steps{
            sh 'sleep 5'
            sh 'mvn test'
        }
    }
                stage('5. PackageCode'){
        steps{
            sh 'mvn package'
        }
    }
}
}
