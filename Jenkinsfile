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
		sh ""
		if sudo netstat -tulpn | grep -q ":8070"; then
		    echo "Port 8080 in use, killing process..."
		    sudo fuser -k 8070/tcp || true
		else
	            echo "Port 8080 free, starting calculator..."
   	 	    sudo cp build/calculator-${env.VERSION} /opt/goapp/
    		    sudo chmod +x /opt/goapp/calculator-${env.VERSION}
   	            cd /opt/goapp
     		    sudo nohup ./calculator-${env.VERSION} > /var/log/calculator.log 2>&1 &
		fi
		"""
        	}
	    }
	}
  }
} 
    



