#!groovy
node ('master') {
	try {
		stage('Preparation') {
		  git branch: 'master', url: 'git@github.com:vreddy-devops/version-test.git'
		  
   		}
	    stage('Version') {
	          dir('verifyJenkins') {
			  
			// def readConfigFile = readFile "gradle/configurations.gradle"
		        File readConfigFile = new File('/var/lib/jenkins/workspace/test-version/verifyJenkins/gradle/configurations.gradle').text
		        def configLines = readConfigFile.readLines()
			  println configLines
		    //    configLines.each { String line ->
        	//	    if (line.contains("versionName")) {
            	//		configVersion = line =~ /(\d+\.)(\d+\.)(\d+)/
            	//		println "CONFIG VER: = " + configVersion[0][0]
		//		        env.VERSION_NAME = configVersion[0][0]
        	//	    }
                  //  else {
                    //    env.VERSION_NAME = "7.5.0"
                  //  }
		    //    }
	        }
	    }

        stage('TestVersion') {
            
            dir('verifyJenkins') {
                sh """
                    test=${env.VERSION_NAME}
                    echo \$test
                """
            }
        }

    }
  catch (ex) {
        currentBuild.result = "FAILED"
        throw ex
    }
} 
