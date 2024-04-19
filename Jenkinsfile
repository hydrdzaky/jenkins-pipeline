pipeline{
    environment{ //PIPELINE ENVIRONMENT VARIABLES
        AUTHOR = "Haydar Dzaky"
        EMAIL = "haydar.dzaky@gmail.com"
    }

    parameters{ //PIPELINE PARAMETERS
        string(name: "NAME", defaultValue: "Guest", description: "what is your name?")
        text(name: "DESCRIPTION", defaultValue: "Guest", description: "tell me about you?")
        booleanParam(name: "DEPLOY", defaultValue: false, description: "Need to deploy?")
    }

    // options{ //PIPELINE OPTIONS
    //     disableConcurrentBuilds()
    //     timeout(time: 10, unit: 'MINUTES')
    // }

    // trigger{ //build trigger
    //     cron("*/5 * * * *")
    // }

    agent none
    stages{
        stage("os setup"){
            matrix{
                axes{
                    axis{
                        name 'OS'
                        values 'ubuntu-1604', 'ubuntu-1804', 'ubuntu-2004'
                    }
                    axis{
                        name 'JAVA'
                        values 'java-8', 'java-11', 'java-17'
                    }
                }
                stages{
                    stage("os setup"){
                        agent {
                            node{ //agent perstage
                                label 'ubuntu-1604 && java-11'
                            }
                        }
                        steps{
                            echo ("setup ${OS} and ${JAVA}") 
                        }
                    }
                }
            }
        } 
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
        environment{ //PIPELINE ENVIRONMENT VARIABLES
            APP = credentials("id-haydar") //CREDENTIALS
        }
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
            sh('./mvnw clean compile test-compile') //command
            echo 'finish build'
            }
        }
        stage('test'){
            agent {
                node{ //agent perstage
                    label 'ubuntu-1604 && java-11'
                }
            }
            steps{ //utility steps
                script{
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
            input{ //input
                message "can we deploy?"
                ok "yes"
                submitter "haydar"
                parameters{
                    choice(name: 'TARGET_ENV', choices: ['DEV', 'QA','PROD'], description:'we will deploy to?')}
            }
            agent {
                node{ //agent perstage
                    label 'ubuntu-1604 && java-11'
                }
            }
            steps{
            echo "deploy to ${TARGET_ENV}"
            }
        }
        stage('release'){
            when{
                expression{
                    return params.DEPLOY
                }
            }
            agent {
                node{ //agent perstage
                    label 'ubuntu-1604 && java-11'
                }
            }
            steps{
            withCredentials([usernamePassword(
                credentialsID : "id-haydar",
                usernameVariable : "USER",
                passwordVariable : "PASSWORD"
            )]){
                     sh('echo "Release it -p $PASSWORD  -u $USER" > "password2.txt"' )
                }
            }
        }
        stage("parameter"){
            agent {
                node{ //agent perstage
                    label 'ubuntu-1604 && java-11'
                }
            }
            steps{ //parameter
                echo "name : ${params.NAME}"
                echo "description : ${params.DESCRIPTION}"
                echo "deploy : ${params.DEPLOY}"
            }
        }
    }
    post{//post actions
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