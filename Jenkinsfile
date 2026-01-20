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
	stage("Archive") {
    	steps {
        script {
            def version = ""

            if (env.TAG_NAME) {
                version = "${env.TAG_NAME}"
            } else if (env.BRANCH_NAME) {
                version = "${env.BRANCH_NAME}-${env.BUILD_NUMBER}"
            } else {
                version = "dev-${env.BUILD_NUMBER}"
            }

            sh """
                mv build/calculator build/calculator-${version}
            """

            archiveArtifacts artifacts: "build/calculator-${version}*", fingerprint: true
            echo "Archiving calculator-${version}"
       	     }
	}
    }
	stage("Deploy"){
		steps{
		script{
		
		def version="dev-${env.BUILD_NUMBER}"
		sh '''
		 sudo cp build/calculator-${version} /opt/goapp 
		 
		sudo chmod +x /opt/goapp/calculator-${version}
		cd /opt/goapp 
		nohup  ./calculator-${version} &
		'''
        	}
	    }
	}
  }
} 
    



