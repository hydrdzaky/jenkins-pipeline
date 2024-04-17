pipeline{
    environment{ //ENVIRONENT
        AUTHOR = "Haydar Dzaky"
        EMAIL = "haydar.dzaky@gmail.com"
        //ENVIRONENT CREDENTIALS
        APP = credentials("id-haydar")
    }
    agent none
    stages{
        stage('hello'){
            agent {
                node{ //agent perstage
                    label 'ubuntu-1604 && java-11'
                }
            }
            steps{
                echo 'Hello Haydar!'
            }
        }
        stage('prepare'){
            agent {
                node{ //agent perstage
                    label 'ubuntu-1604 && java-11'
                }
            }
            steps{ 
                echo("author : ${AUTHOR}")
                echo("email : ${EMAIL}")
                echo("app user : ${APP_USR}")
                echo("app password : ${APP_PSW}")
                sh('echo "app password :$APP_PSW" > "password.txt"' )
                
                //variable env
                echo ("start job : ${env.JOB_NAME}")
                echo ("start job : ${env.BUILD_NUMBER}")
                echo ("start job : ${env.BRANCH_NAME}")
            }
        }
        stage('build'){
            agent {
                node{ //agent perstage
                    label 'ubuntu-1604 && java-11'
                }
            }
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
            agent {
                node{ //agent perstage
                    label 'ubuntu-1604 && java-11'
                }
            }
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
            agent {
                node{ //agent perstage
                    label 'ubuntu-1604 && java-11'
                }
            }
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