pipeline{
    agent{
        docker{
            image 'maven:3.8.1-adoptopenjdk-11'
            args '-v /root/.m2:/root/.m2'
        }
    }
    options{
        skipStagesAfterUnstable()
    }
    stages{
        stage("Build"){
            steps{
                echo "========executing Build========"
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test'){
            steps{
                echo "========executing Test========"
                sh 'mvn test'
            }
            post{
                always{
                    junit "target/surefire-reports/*.xml"
                }
                success{
                    echo "====++++Test executed successfully++++===="
                }
                failure{
                    echo "====++++Test execution failed++++===="
                }
        
            }
        }
        stage('Deploy'){
            steps{
                echo "========executing Deploy========"
                sh './jenkins/scripts/deliver.sh'
            }
            post{
                always{
                    echo "===== ...... _____"
                }
                success{
                    echo "====++++Deploy executed successfully++++===="
                }
                failure{
                    echo "====++++Deploy execution failed++++===="
                }
        
            }
        }
    }
}