pipeline {
  agent any  
  
  environment {                
         SONAR_HOME =  tool name: 'sonar-scanner'
    }

//   stages {
//     stage('Build'){
//             steps{
           
//                 sh 'echo export MAVEN_HOME= "{env.$MAVEN_HOME}"'
               
//                 sh'''
                
//                 export PATH=$PATH:$MAVEN_HOME/bin
//                 mvn clean package
                
                
//                  '''

//             }
//          }
         
    stage('Scan') {
      steps {
         withSonarQubeEnv('sonarqube-server') { 
             

            sh 'echo export SONAR_HOME= "{env.$SONAR_HOME}"'   
            sh '''
        
                    export PATH=$PATH:$SONAR_HOME/bin

                      sonar-scanner \
                      -Dsonar.projectKey=jskey \
                      -Dsonar.sources=. \
                      -Dsonar.host.url=http://192.168.100.115:9000 \
                      -Dsonar.login=b30981b3ff3768305a8f05253b95886320794b0f
              '''
        
        }
      }
    }
   stage('Dependency Check Report') {
    steps {
        dependencyCheck additionalArguments: ''' 
            -o "./" 
            -s "./"
            -f "ALL" 
            --prettyPrint''', odcInstallation: 'Dependency-Check'
        dependencyCheckPublisher pattern: 'dependency-check-report.xml'
          }    
    }
  }

