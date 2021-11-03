pipeline{
    agent any
    tools{
        jdk 'myjava'
        maven 'mymaven'
    }
    environment{
        NEW_VERSION='1.4.0'
    }
    stages{
        stage("COMPILE"){
            steps{
                script{
                     echo "Compiling the code"
                     git 'https://github.com/preethid/addressbook.git'
                     sh 'mvn compile'
                }
            }
                    }
        stage("UnitTest"){
             when{
            expression{
                BRANCH_NAME =='master'
            }
             }
              steps{
                script{
             echo "Run the unit test"
             sh 'mvn test'
        }
              }
              post{
                  always{
                      junit 'target/surefire-reports/*.xml'
                  }
              }
        }
        stage("Package"){
              steps{
                script{
              echo "Building the app"
              echo "building version ${NEW_VERSION}"
              sh 'mvn package'
        }
    }
        }
    stage("Deploy"){
        when{
            expression{
                BRANCH_NAME =='master'
            }
        }
        steps{
            script{
                echo "Deploying the app"
                echo "Deploying ${NEW_VERSION}"
            }
        }
    }
    }
}
