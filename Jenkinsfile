pipeline{
    agent any
      tools{ 
          go 'go-1.21'
      }
      stages{
        stage("build"){
          step{
            echo "i am building"
          }
      }
       stage("test"){
          step{
            echo "testing"
          }
      }
      stage("lint"){
          step{
            echo "linting"
          }
      }
      stage("Archive"){
          step{
            echo "archiving this program"
          }
       }
      stage("deploy"){
        step{
          echo "deploying"
        }
    }
  }
} 
    



