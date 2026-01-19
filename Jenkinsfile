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
		scripts{
		def version= ""
		if (env.TAG_NAME){
			version="${env.TAG_NAME}"
		}
		else if (env.BRANCH_NAME){
			version="${env.BRANCH_NAME}"-"{env.BUILD_NUMBER}"
		}
		else{
			version="dev-${env.BUILD_NUMBER}"
		}
	    sh "mv calculator calculator-${version}"
            archiveArtifacts artifacts:"build/calculator-${version}*", fingerprint:true
            echo "archiving this program"
          }
       }
}
      stage("deploy"){
        steps{
          echo "deploying"
        }
    }
  }
} 
    



