pipeline{
    agent {
        node{
            label 'ubuntu-1604 && java-11'
        }
    }
    stages{
        stage('hello'){
            steps{
                echo 'Hello Haydar!'
            }
        }
        stage('build'){
            steps{
                script{ //script
                    for(int i=0;i<5;i++){
                        echo("scripy ${i}")
                    }
                }
            echo 'start build'
            sh('./mvnw clean compile test-compile')
            echo 'finish build'
            }
        }
        stage('test'){
            steps{
                
                script{ //utility steps
                    def data =[
                        "firstName" : "Haydar",
                        "lastName" : "Dzaky"
                    ]
                    writeJSON(file:"data.json", json:data)
                }
            echo 'start test'
            sh('./mvnw test')
            echo 'finish test'
            }
        }
        stage('deploy'){
            steps{
            echo 'deploy'
            }
        }
    }
    post
    {
        always{
            echo 'Goodbye Haydar!'
        }
        success{
            echo 'Success!'
        }
        failure{
            echo 'Failure!'
        }
    }
}