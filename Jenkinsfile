pipeline{
    tools{
        maven 'MyMaven'
    }
agent{
    label 'workernode1'
}
stages{
    stage('1. CloneGitRepo'){
        parallel{
             stage('GitCloneMaster'){
                 agent {
                     label 'workernode1'
                 }
                steps{
                    sh 'echo "Hostname: `hostname` Date: `date`"'
                    git 'https://github.com/jsinghjbd/DevOpsCodeDemo.git'
                }
            }
            stage('GitCloneWorker'){
                 agent {
                     label 'workernode2'
                 }
                steps{
                    sh 'echo "Hostname: `hostname` Date: `date`"'
                    git 'https://github.com/jsinghjbd/DevOpsCodeDemo.git'
                }
            }
        }
    }
    stage('Parallel Stages')
    {
        parallel{
             stage('2. BuildCode'){
                 agent {
                     label 'workernode1'
                 }
                steps{
                    sh 'sleep 15'
                    sh 'echo "`hostname`"'
                    sh 'mvn compile'
                    
                }
            }
            stage('3. ReviewCode'){
                agent {
                     label 'workernode1'
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
