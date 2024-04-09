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
            echo 'build 1'
            echo 'build 2'
            echo 'build 3'
            }
        }
        stage('test'){
            steps{
            echo 'test'
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