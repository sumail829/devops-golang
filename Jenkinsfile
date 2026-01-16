pipeline{
    agent any
      tools{ 
          go 'go-1.21'
      }
      stages{
        stage("build"){
          steps{
            echo "i am building"
          }
      }
       stage("test"){
          steps{
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
    



