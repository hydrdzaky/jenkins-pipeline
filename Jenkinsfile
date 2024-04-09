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
}
}