pipeline{
    agent any
      tools{ 
          go 'go1.23.10'
      }
      stages{
        stage("build"){
          steps{
            sh '''
              mkdir -p build
              go build -o build/calculator 
              '''
            echo "i am building"
          }
      }
       stage("test"){
          steps{
           sh "go test ./..."
            echo "testing"
          }
      }
      stage("lint"){
          steps{
            echo "linting"
          }
      }
      stage("Archive"){
          steps{
            archiveArtifacts artifacts:"build/calculator*", fingerprint:true
            echo "archiving this program"
          }
       }
      stage("deploy"){
        steps{
          echo "deploying"
        }
    }
  }
} 
    



