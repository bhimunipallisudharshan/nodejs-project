def registry ='https://artifact12345.jfrog.io/ '
def imageName = 'artifact12345.jfrog.io/dockerbuild-docker-local/demo-nodejs'
def version   = '1.0.2'
pipeline{
    agent {
        node {
            label "valaxy"
        }
    }
    tools {nodejs 'Nodejs 16.6.0'}

    stages {
          stages {
         stage('git clone') {
            steps{
              git branch: 'main', url: 'https://github.com/bhimunipallisudharshan/nodejs-project.git'
        }
      }
        stage('build') {
            steps{
                echo "------------ build started ---------"
               	sh "npm install"
                echo "------------ build completed ---------"
        }
      }

        stage('Unit Test') {
            steps {
                echo '<--------------- Unit Testing started  --------------->'
                sh 'npm test'
                echo '<------------- Unit Testing stopped  --------------->'
            }
        }

stage(" Docker Build ") {
      steps {
        script {
           echo '<--------------- Docker Build Started --------------->'
           app = docker.build(imageName+":"+version)
           echo '<--------------- Docker Build Ends --------------->'
        }
      }
    }

    stage (" Docker Publish "){
        steps {
            script {
               echo '<--------------- Docker Publish Started --------------->'  
                docker.withRegistry(registry, 'jfrog1'){
                    app.push()
                }    
               echo '<--------------- Docker Publish Ended --------------->'  
            }
        }
    }
           // stage('Deployment') {
            //steps {
              //  echo '<--------------- deployment started  --------------->'
                //sh './deploy.sh'
                //echo '<------------- deployment stopped  --------------->'
            //}
        }  
    }
    }
