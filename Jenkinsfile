pipeline {
    agent  any;
    stages {
        //stage('Preparing the environment') {
        //    steps {
        //        //sh 'python3 -m pip install -r requirements.txt'
        //        sh 'sudo apt-get install -y python3-pylint python3-pytest'
        //    }
        //}
        stage('Code Quality') {
            steps {
                sh 'python3 -m pylint app.py'
            }
        }
        stage('Tests') {
            steps {
                sh 'python3 -m pytest'
            }
        }
   
    stage('Build') {
          agent { 
            node{
              label "DockerServer"; 
              }
          }
          steps {
              sh 'docker build -t chapter10:latest https://github.com/vladvidov/Chapter10.git'
          }
      }        
      stage('Deploy') {
          agent { 
            node{
              label "DockerServer"; 
              }
          }
          steps {
              sh 'docker run -tdi -p 5000:5000 chapter10:latest'
          }
      }
    }

}

